# Atomic Operations

Atomic operations in concurrent programming are program operations that run completely independently
of any other processes.

## Problem

We cannot warrant what file will exist when it is started reading. It might be removed, because
we cannot adjust tasks queque.

```js
server.on('request', (req, res) => {
  const pathname = url.parse(req.url).pathname.slice(1);
  const filepath = path.join(__dirname, 'files', pathname);

  switch (req.method) {
    case 'GET':
      fs.stat('file.txt', (error, fileStat) => {
        if (err.code === 'ENOENT') {
          res.statusCode = 404;
          res.end('not found');
        }
        if (fileStat.isFile()) {
          fs.createReadStream('file.txt').pipe(res);
        }
      });
      break;
    case 'DELETE':
      fs.unlink(filepath, (err) => {
        if (err) {
          if (err.code === 'ENOENT') {
            res.statusCode = 404;
            res.end('file not found');
          } else {
            res.statusCode = 500;
            res.end('internal server error');
          }
        } else {
          res.end('ok');
        }
      });
      break;
    default:
      res.statusCode = 501;
      res.end('Not implemented');
  }
});
```

## Test

It might be failed or might be passed.

```js
it('Complex case', async () => {
  const content = fs.readFileSync(path.join(__dirname, '../files/1.txt'));

  const [r1, r2] = await Promise.all([
    axios.get('http://localhost:3000/1.txt'),
    axios.delete('http://localhost:3000/1.txt'),
  ]);

  assert.strictEqual(content.toString('utf-8'), r1.data);

  assert.strictEqual(r2.data, 'ok');
  assert.strictEqual(fs.existsSync(path.join(__dirname, '../files/1.txt')), false);
});
```

## Solution

```js
server.on('request', (req, res) => {
  const pathname = url.parse(req.url).pathname.slice(1);
  const filepath = path.join(__dirname, 'files', pathname);

  switch (req.method) {
    case 'GET':
      fs.createReadStream(filepath)
          .on('error', (err) => {
            if (err.code === 'ENOENT') {
              res.statusCode = 404;
              res.end('not found');
            } else {
              res.statusCode = 500;
              res.end('internal error');
            }
          })
          .pipe(res);
      break;
    case 'DELETE':
      fs.unlink(filepath, (err) => {
        if (err) {
          if (err.code === 'ENOENT') {
            res.statusCode = 404;
            res.end('file not found');
          } else {
            res.statusCode = 500;
            res.end('internal server error');
          }
        } else {
          res.end('ok');
        }
      });
      break;
    default:
      res.statusCode = 501;
      res.end('Not implemented');
  }
});
```
