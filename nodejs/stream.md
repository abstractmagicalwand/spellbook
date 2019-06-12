# Stream

A stream is an abstract interface for working with streaming data in Node.js.

They were introduced in the Unix operating system decades ago, and programs can interact with each
other passing streams through the pipe operator `|`.

```sh
cat path/to/file | grep search_string
```

For example, in the traditional way, when you tell the program to read a file, the file is read into
memory, from start to finish, and then you process it.

Using streams you read it piece by piece, processing its content without keeping it all in memory.

For instance:

1. The Internet.
2. Pipe operator in unix.
3. `process.stdout`, `process.stdin`
4. `fs.ReadStream`, `fs.WriteStream`, `http.IncomingMessage`, `http.ServerResponse`
5. etc.

## Types of Streams

1. **Writable** - streams to which data can be written (for example, `fs.createWriteStream()`).
2. **Readable** - streams from which data can be read (for example, `fs.createReadStream()`).
3. **Duplex** - streams that are both Readable and Writable (for example, `net.Socket`).
4. **Transform** - Duplex streams that can modify or transform the data as it is written and read
  (for example, `zlib.createDeflate()`).

## Get chunk from readable stream

Readable stream have two state. They are **flowing and paused. To switch state from paused to flowing:

1. `readable.pipe(outStream)`
2. `readable.on('data', (chunk) => {...})`
3. `readable.resume()` and `readable.pause()`

## Implement pipe

```js
streamIn.on('data', (chunk) => {
  const isWillingMore = streamOut.write(chunk);

  if (isWillingMore) {
    return;
  }

  streamIn.pause();

  streamOut.once('drain', () => {
    streamIn.resume();
  });
});

streamIn.on('end', () => {
  streamOut.end();
});

streamIn.on('error', (error) => {});
```

## Error handling

```js
fileIn
    .on('error', cleanup)
    .pipe(gzip)
    .on('error', cleanup)
    .pipe(fileOut)
    .on('error', cleanup);

function cleanup(error) {
  fileIn.destroy();
  fileOut.destroy();
}
```

Better:

```js
stream.pipeline(
    fileIn, gzip, fileOut,
    (error) => {
      if (error) {
        cleanup(error);
      } else {
        console.log('done');
      }
    }
);
```

Better:

```js
const pipeline = promisify(stream.pipeline);

pipeline(fileIn, gzip, fileOut)
    .then(() => console.log('done'))
    .catch(cleanup);
```

## When pipeline don't work

```js
// https://github.com/nodejs/node/pull/26638

const {Readable, Writable, pipeline} = require('stream');

const read = new Readable({
  read() {},
});

const write = new Writable({
  emitClose: false,
  write(data, enc, cb) {
    cb();
  },
});

setImmediate(() => read.destroy());

pipeline(read, write, (err) => {
  // this never be called because `write` won't emit 'close'
  console.log('done', err);
});
```

## Set header before work with stream

```js
const stream = fs.createReadStream('big.png');
stream.on('open', () => {
  res.setHeader('Content-Type', 'image/png');
});
stream.pipe(res);
```

## Event `finish` and `end` is the same

`finish` for Writable stream. `end` for Readable stream. They have different name because Duplex
stream are Readable and Writable.

## Duplex

net.Socket instances are Duplex streams whose Readable side allows consumption of data received from
the socket and whose Writable side allows writing data to the socket. Because data may be written to
the socket at a faster or slower rate than data is received, it is important for each side to
operate (and buffer) independently of the other.

## API for Stream Implementers

### Transform

All Transform stream implementations must provide a `_transform()` method to accept input and
produce output. The `transform._transform()` implementation handles the bytes being written, computes
an output, then passes that output off to the readable portion using the `readable.push()` method.

Custom Transform implementations may implement the `transform._flush()` method. This will be called
when there is no more written data to be consumed, but before the 'end' event is emitted signaling
the end of the Readable stream.

## Details

- [Nodejs Docs - Stream](https://nodejs.org/dist/latest/docs/api/stream.html)
- [Node.js streams cheatsheet](https://devhints.io/nodejs-stream)
- [Streams handbook](https://github.com/substack/stream-handbook)
