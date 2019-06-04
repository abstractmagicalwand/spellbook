# Promises

```js
const promise = new Promise(function(resolve, reject) {
  // The executor.
  // 1. The executor is called automatically and immediately (by the `new Promise`).
  // 2. The executor receives two arguments: `resolve` and `reject`.
});

// We can’t directly access them from our "consuming code".
// {
//   [[PromiseStatus]]: "pending",
//   [[PromiseValue]]: undefined
// }
```

Afer call `resolve(value)`:

```js
// {
//   [[PromiseStatus]]: "resolved",
//   [[PromiseValue]]: value
// }
```

Or afer call `reject(error)`:

```js
// {
//   [[PromiseStatus]]: "rejected",
//   [[PromiseValue]]: error
// }
```

Promises can change only one time.

## API

### `Promise.resolve(value)`

It returns a resolved promise with the passed value. The method is used when we already have a value,
but would like to have it "wrapped" into a promise. For instance, [Caching](../recipes/caching.md)

### `Promise.resolve(error)`

It returns a rejected promise with the passed error.

### `Promise.all(promises)`

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
    urls.map((url) => fetch(url).catch((error) => error))
);
```

### `Promise.race(promises)`

It takes an iterable of promises, but instead of waiting for all of them to finish, it waits for the
first result (or error), and goes on with it. After the first settled promise "wins the race", all
further results/errors are ignored.

## then, catch, finally

### `.then` always return promise

- `return value` returns resolved promise.
- `throw error` returns rajected promise.
- `return promise` returns pending promise.

### Add many `.then` and chaining aren't the same

```js
const promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000);
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});

promise.then(function(result) {
  alert(result); // 1
  return result * 2;
});
```

```js
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000);
}).then(function(result) {
  alert(result); // 1
  return result * 2;
}).then(function(result) {
  alert(result); // 2
  return result * 2;
}).then(function(result) {
  alert(result); // 4
  return result * 2;
});
```

### finally

1. A `finally` handler has no arguments.
2. A `finally` handler passes through results and errors to the next handler.
3. `.finally(f)` is a more convenient syntax than `.then(f, f)`: no need to duplicate the function `f`.

```js
new Promise((resolve, reject) => {
  /* do something that takes time, and then call resolve/reject */
})
    // runs when the promise is settled, doesn't matter successfully or not
    .finally(() => {/* stop loading indicator */})
    .then((result) => {/* show result */}, (err) => {/* show error */});
```

### Thenables

`.then` may return an arbitrary "thenable" object, and it will be treated the same way as a promise.

```js
class Thenable {
  constructor(num) {
    this.num = num;
  }
  then(resolve, reject) {
    alert(resolve); // function() { native code }
    // resolve with this.num*2 after the 1 second
    setTimeout(() => resolve(this.num * 2), 1000);
  }
}

new Promise((resolve) => resolve(1))
    .then((result) => new Thenable(result))
    .then(alert); // shows 2 after 1000ms
```

## Details

- [Promises, async/await](http://javascript.info/async)
- [Promises vs Callbacks](https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#what-are-the-pros-and-cons-of-using-promises-instead-of-callbacks)
