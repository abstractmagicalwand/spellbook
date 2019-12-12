# Array

## array.slice vs array.splice

```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
const months = ['Jan', 'March', 'April', 'June'];

// 1) splice mutates original array
console.log(animals.slice(1, 3)); // ['bison', 'camel']
console.log(months.splice(1, 2)); // ['March', 'April']

console.log(animals); // ['ant', 'bison', 'camel', 'duck', 'elephant']
console.log(months); // ['Jan', 'June']

// 2) splice can add elements
console.log(months.splice(1, 0, 'March', 'April')); // []
console.log(months); // ['Jan', 'March', 'April', 'June']
```
