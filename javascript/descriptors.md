# Descriptors

It's a configuration of property. We can change property behavior.

Descriptor example:

```json
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
```

## Get descriptor

```js
let user = {
  name: "John"
};

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');
```

If we have lots of properties:

```js
Object.getOwnPropertyDescriptor(user); // {name: descriptor}
```

## Set descriptor

```js
let user = {};

Object.defineProperty(user, "name", {
  value: "John"
});

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

/*
{
  "value": "John",
  "writable": false,
  "enumerable": false,
  "configurable": false
}
 */
```

If we have lots of properties:

```js
Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});
```

## Writable

We can make read-only property.

```js
let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  writable: false
});

user.name = "Pete";
```

> In the non-strict mode, no errors occur when writing to read-only properties and such. But the
operation still won’t succeed. Flag-violating actions are just silently ignored in non-strict.

## Enumerable

```js
let user = {
  name: "John",
  toString() {
    return this.name;
  }
};

Object.defineProperty(user, "toString", {
  enumerable: false
});

for (let key in user) {
  console.log(key); // only name
}
```

## Configurable

```js
let user = { };

Object.defineProperty(user, "name", {
  value: "John",
  writable: false,
  configurable: false
});

// won't be able to change user.name or its flags
// all this won't work:
//   user.name = "Pete"
//   delete user.name
//   defineProperty(user, "name", ...)
Object.defineProperty(user, "name", {writable: true});
// Uncaught TypeError: Cannot redefine property: name
```

## Other methods

- `Object.preventExtensions(obj)` forbids the addition of new properties to the object.
- `Object.seal(obj)` forbids adding/removing of properties. Sets `configurable: false` for all
existing properties.
- `Object.freeze(obj)` forbids adding/removing/changing of properties. Sets
`configurable: false, writable: false` for all existing properties.

And test methods:

- `Object.isExtensible(obj)`
- `Object.isSealed(obj)`
- `Object.isFrozen(obj)`

## Details

- [Property flags and descriptors](http://javascript.info/property-descriptors#sealing-an-object-globally)
