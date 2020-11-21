# Debugging

- [Debugging Guide](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [Netflix JavaScript Talks - Debugging Node.js in Production (MUST SEE!) 👀](https://youtu.be/O1YP8QP9gLA)

## Profiling

- [Speedscope is a fast, interactive web-based viewer for performance profiles](https://github.com/jlfwong/speedscope#usage)
- [Flame graphs are a visualization of profiled software](https://github.com/brendangregg/FlameGraph)

### Memory leak

- `ab -n 10 -c 1 http://localhost:3000/users` sends a bunch of request.
- `process.memoryUsage().heapUsed` shows used heap.
- [Take heap snapshots](https://medium.com/tech-tajawal/memory-leaks-in-nodejs-quick-overview-988c23b24dba)
- [The --heapsnapshot-near-heap-limit Flag Coming to Node](https://twitter.com/JoyeeCheung/status/1319002537563885568)

## Chrome DevTools

1. Run application: `node --inspect index.js`.
2. Open in chromium: `chrome://inspect`.
3. Click the `Open dedicated DevTools for Node` link.

## VSCode

- [Configuration](https://gist.github.com/abstractmagicalwand/f9d62e85db7d05302db87006a6f6f4c2#file-launch-json)
- [Wich Docker](https://gist.github.com/abstractmagicalwand/043499de2273e35d8c29d0d1b6a42d79)

## Curl

```text
-i, --include       Include protocol response headers in the output
-d, --data <data>   HTTP POST data
```

## Other

- [Nodemon](https://github.com/remy/nodemon)
- [Postman](https://www.getpostman.com/)
- [Hoppscotch](https://github.com/hoppscotch/hoppscotch)
- [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)
