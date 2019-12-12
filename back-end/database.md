# Database

- [How Does a Database Work?](https://cstack.github.io/db_tutorial/)

## Migration

A migration is performed on a database whenever it is necessary to update or revert that data or schema
to some newer or older version.

You should make backup for database before starting migration.

## Transaction

When a transaction commits, all data changes made in the transaction are saved. If any operation in
the transaction fails, the transaction aborts and all data changes made in the transaction are discarded
without ever becoming visible.

## Relationship

It is a situation that exists between two relational database tables when one table has a foreign key
that references the primary key of the other table. Relationships allow relational databases to split
and store data in different tables, while linking disparate data items.
