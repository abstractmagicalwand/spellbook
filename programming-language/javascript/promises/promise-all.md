# `Promise.all(promises)`

It accepts an iterable of promises and returns a new promise. But if any of those objects is not
a promise, it’s wrapped in `Promise.resolve`.

The new promise resolves when all listed promises are settled and has an iterable of their results.

The rejection error becomes the outcome of the whole Promise.all. The **important detail** is that
promises provide no way to "cancel" or "abort" their execution. So other promises continue to
execute, and then eventually settle, but all their results are ignored. We can write additional code
to handle it in case of an error or we can make errors show up as members in the resulting iterable:

```js
// Fault-tolerant Promise.all
Promise.all(
    urls.map((url) => fetch(url).catch((error) => error)),
);
```
