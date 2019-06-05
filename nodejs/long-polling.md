# Long polling

1. A client requests a webpage from a server using regular HTTP.
2. The client receives the requested webpage and executes the JavaScript on the page which requests
a file from the server.
3. The server does not immediately respond with the requested information but waits until there's
new information available.
4. When there's new information available, the server responds with the new information.
5. The client receives the new information and immediately sends another request to the server,
re-starting the process.

## Client

```js
subscribe();

function subscribe() {
  const xhr = new XMLHttpRequest();

  xhr.open('GET', '/subscribe?r=' + Math.random(), true);

  xhr.onload = function() {
    if (xhr.status != 200) {
      return this.onerror();
    }

    const li = document.createElement('li');
    li.textContent = this.responseText;
    messages.appendChild(li);

    subscribe();
  };

  xhr.onerror = xhr.onabort = function() {
    setTimeout(subscribe, 500);
  };

  xhr.send();
}
```

## Server

```js
const clients = new Set();

router.get('/subscribe', async (ctx, next) => {
  const message = await new Promise((resolve, reject) => {
    clients.push(resolve);

    ctx.res.on('close', function() {
      clients.remove(resolve);
      resolve();
    });
  });

  ctx.body = message;
});

router.post('/publish', async (ctx, next) => {
  const message = ctx.request.body.message;

  if (!message) {
    ctx.throw(400, 'required field `message` is missing');
  }

  clients.forEach((resolve) => {
    resolve(message);
  });

  clients.clear();

  ctx.body = 'ok';
});
```
