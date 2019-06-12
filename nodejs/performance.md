# Performance

- [Netflix JavaScript Talks - Debugging Node.js in Production (MUST SEE!) 👀](https://youtu.be/O1YP8QP9gLA)

## Memory leak

- `ab -n 10 -c 1 http://localhost:3000/users` sends a bunch of request.
- `process.memoryUsage().heapUsed` shows used heap.
- [Take heap snapshots](https://medium.com/tech-tajawal/memory-leaks-in-nodejs-quick-overview-988c23b24dba)
