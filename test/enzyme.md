# Enzyme

## How to debug selecting element

```js
console.log(
    wrapper
        .find('div')
        .children()
        .last()
        .children()
        .first()
        .debug(),
);
```
