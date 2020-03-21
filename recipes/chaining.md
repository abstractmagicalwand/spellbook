# Chaining

```js
class Rabbit {
  run() {
    console.log('Rabbit is running');
    return this;
  }

  stop() {
    console.log('Rabbit has stopped');
    return this;
  }

  walk() {
    console.log('Rabbit is walking');
    return this;
  }
}

const rabbit = new Rabbit();

rabbit
    .run()
    .stop()
    .walk()
    .run()
    .stop()
    .walk();

// Rabbit is running
// Rabbit has stopped
// Rabbit is walking
// Rabbit is running
// Rabbit has stopped
// Rabbit is walking
```

## Examples

- [Check if a number is equal to 13](https://github.com/jezen/is-thirteen)
