# Jest

## Mock different properties for the same module

```js
beforeEach(() => jest.resetModules());

it('returns galician for hi', () => {
  jest.mock('./appEnv', () => ({
    currentLanguage: 'GL',
  }));
  const {hello} = require('./greetings');
  expect(hello()).toEqual('Ola!');
});

it('returns hi', () => {
  jest.mock('./appEnv', () => ({currentLanguage: 'EN'}));
  const {hello} = require('./greetings');
  expect(hello()).toEqual('Hi!');
});
```
