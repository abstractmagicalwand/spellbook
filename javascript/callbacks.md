# Callbacks

```js
function loadScript(src) {
  const script = document.createElement('script');
  script.src = src;

  document.head.append(script);
}

// loads and executes the script
loadScript('/my/script.js'); // the script has "function newFunction() {…}"

// the code below loadScript doesn't wait for the script loading to finishs
newFunction(); // Uncaught ReferenceError: newFunction is not defined
```

```js
function loadScript(src, callback) {
  const script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript('/my/script.js', () => {
  // the callback runs after the script is loaded
  newFunction(); // so now it works
});
```

## Error-first callback

1. The first argument of the callback is reserved for an error if it occurs. Then callback(err) is called.
2. The second argument (and the next ones if needed) are for the successful result.
Then callback(null, result1, result2…) is called.

```js
function loadScript(src, callback) {
  const script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}

loadScript('/my/script.js', (err, script) => {
  if (err) {
    // handle error
  } else {
    // script loaded successfully
  }
});
```

## Callback hell

```js
loadScript('1.js', (err, script) => {
  if (err) {
    handleError(err);
  } else {
    loadScript('2.js', (err, script) => {
      if (err) {
        handleError(err);
      } else {
        loadScript('3.js', (err, script) => {
          if (err) {
            handleError(err);
          } else {
            // ...continue after all scripts are loaded
          }
        });
      }
    });
  }
});
```

## Details

- [Callbacks](http://javascript.info/callbacks)
