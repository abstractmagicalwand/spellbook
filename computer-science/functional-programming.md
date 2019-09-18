# Functional programming

## Memoization

In computing, memoization or memoisation is an optimization technique used primarily to speed up
computer programs by storing the results of expensive function calls and returning the cached result
when the same inputs occur again.

[Caching](../recipes/caching.md)

## Referential transparency

```js
function half(n) {
  return n / 2;
}
```

Output (return) must be the same for the same input (arguments). For example, we could replace
`half(8)` with `4` wherever used in our code with no change to the final outcome. This is called
**referential transparency**.

Referential transparency also enables **memoization**.

## Side Effects

When a function or expression modifies state outside its own context, the result is a **side effect**.
Examples of side effects include making a call to an API, manipulating the DOM, raising an alert
dialog, writing to a database, etc.

Functions that cause side effects are less predictable and harder to test since they result in changes
outside their local scope.

## Pure function

1. Its evaluation must have no side effects.
2. It must have referential transparency.

## Details

- [Glossary of Modern JavaScript Concepts: Part 1](https://auth0.com/blog/glossary-of-modern-javascript-concepts/)
- [If immutable objects are good, why do people keep creating mutable objects?](https://softwareengineering.stackexchange.com/a/151735)
