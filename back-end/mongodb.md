# MongoDB and Mongoose

## Index

It give possibility to fast find document by indexed field.

### Set index

Use `unique` field. Index will be unique. It is the implisit way:

```js
new mongoose.Schema({
  email: {
    type: String,
    required: 'Укажите email',
    unique: true,
  },
});
```

Use `index` field:

```js
new mongoose.Schema({
  displayName: {
    type: String,
    index: true,
  },
});
```

Use `index` method:

```js
userSchema.index({displayName: 1, age: -1});
```

Value is order sorting.

`1` is ascending.
`-1` is descending.

MongoDB fast finds only for this query-like:

```js
User.find({displayName: 'Ivan', age: 10});
```

## Remove field from document

Use update operator `$unset`:

```js
User.findOneAndUpdate(
    {verificationToken: ctx.request.body.verificationToken},
    {$unset: {verificationToken: ctx.request.body.verificationToken}},
);
```

## Relationship

The first way:

```js
const bookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
  },
});

const Book = mongoose.model('Book', bookSchema);

const authorSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
  },
  books: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Book',
  }],
});

const Author = mongoose.model('Author', authorSchema);
```

This way might be bad when author has a lot of books.

The second way is virtual field:

```js
const bookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
  },
  author: {
    type: String,
  },
});

const Book = mongoose.model('Book', bookSchema);

const authorSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
  },
}, {toJSON: {virtuals: true}, toObject: {virtuals: true}});

authorSchema.virtual('books', {
  ref: 'Book',
  localField: 'name',
  foreignField: 'author',
});

const Author = mongoose.model('Author', authorSchema);
```

**This relation only has got mongoose. MangoDB knows nothing about horse.**

### Get all relations

[Deep (multi-level) populate](http://mongoosejs.com/docs/populate.html#deep-populate)

```js
Author.findOne({name: 'Leo Tolstoy'}).populate('books');
```
