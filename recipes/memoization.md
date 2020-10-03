# Memoization

In computing, memoization or memoisation is an optimization technique used primarily to speed up
computer programs by storing the results of expensive function calls and returning the cached result
when the same inputs occur again.

- [How I wrote the world's fastest JavaScript memoization library](https://community.risingstack.com/the-worlds-fastest-javascript-memoization-library/)

```js
const memoize = (f) => {
  const cache = new Map();

  return (argument) => {
    if (cache.has(argument)) {
      return cache.get(argument);
    }

    const result = f(argument);

    cache.set(argument, result);

    return result;
  };
};
```

## Promise

```js
function loadCached(url) {
  const cache = loadCached.cache || (loadCached.cache = new Map());

  if (cache.has(url)) {
    return Promise.resolve(cache.get(url));
  }

  return fetch(url)
      .then((response) => response.text())
      .then((text) => {
        cache.set(url, text);
        return text;
      });
}
```

## Examples

- [memoize](https://github.com/lodash/lodash/blob/master/memoize.js)
