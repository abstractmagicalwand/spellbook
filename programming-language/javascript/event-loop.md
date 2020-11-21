# Event Loop

- [What the heck is the event loop anyway? | Philip Roberts | JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
- [Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)
- [Асинхронное программирование (полный курс)](https://habr.com/ru/post/452974/)
- [Faster async functions and promises](https://v8.dev/blog/fast-async)

```js
(function() {
  let promise = Promise.reject(new Error("Promise Failed!"));
  setTimeout(() => promise.catch(err => alert('caught')));

  // Error: Promise Failed!
  window.addEventListener('unhandledrejection', event => alert(event.reason));
})()
```
