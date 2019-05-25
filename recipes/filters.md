# Filters

We can avoid duplicated data when using flag.

```js
const filters = {
  name: 'Alex',
};

userList.map((user) => {
  const isShowed = user.name.includes(filters.name);

  return {...user, isShowed};
});
```
