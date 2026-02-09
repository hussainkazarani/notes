
## Main
> \- PostgreSQL = advanced open-source relational database <br>
> \- strongly typed <br>
> \- very strict (which is good, unlike most humans) <br>
> \- supports JSON, indexing, extensions, transactions <br>
> \- it mainly consists of the Server, Users/Roles, Databases, psql (cli) <br>
> \- the order is as follows: `server` &rarr; `databases` &rarr; `schemas` &rarr; `tables` <br>
> \- databases give hard isolation (app_prod, app_staging), schemas are module splits (auth.users, auth.sessions, billings.invoices) <br>
> \- schema is a namespace folder in postgres db

### Installation
\- we need to install the `PostgreSQL Server` and also `CLI` to use it. It also has a `GUI` called `pgAdmin` <br>
\- it has a default `postgres` user and saves it on your machine <br>
\- to install on mac use:`brew install postgresql@18` or [here](https://postgresapp.com/downloads.html) <br>
\- then add `export PATH="/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH"` to `~/.zshrc`,

### Defaults
Role - `postgres` and `kazarani`(default macOS user) <br>
Database - `postgres`, `kazarani`, `template0`, `template1` <br>
Schema - `public`

## Commands
`psql --version` &rarr; shows postgres version

`\l` &rarr; list databases

`\q` &rarr; quit psql

`\conninfo` &rarr; show current DB and user

`\d`, `\d <tablename>` &rarr; lists all relations (tables, views, sequences, etc) in current db

`\du` &rarr; list users

`\dt` &rarr; list tables in current db

`\dt+` &rarr; list tables with details

`\dv`, `\di`, `\df`, `\dn` &rarr; describe views, indexes, functions, schemas

`\s` &rarr; command history

`\!` &rarr; clear console

## Connections
`psql -h localhost -p 5432 -U alice -d mydb` &rarr; complete connection command

`psql mydb` &rarr; connect to a specific DB shortform (user is OS username)

`\c mydb` &rarr; switch to another database

## Database
`CREATE DATABASE appdb;` &rarr; creating a database (owner is role running the command)

`DROP DATABASE appdb;` &rarr; delete a database

## PostgreSQL Roles, Privileges, Permissions
> **Role** - who you are <br>
> **Privileges** - what you can touch
>
> **PostgreSQL** <br>
> \- creates a role → identity <br>
> \- grants privileges → permissions on objects
>
> **Two different layers** <br>
> \- server level abilities <br>
> \- object level access
>
> **ALTER ROLE/USER** - change role's builtin abilities (server level abilities) <br>
> **GRANT** - give access to specific objects <br>
> **USER** and **ROLE** are the same thing <br>
> **Privileges** and **Permissions** are the same thing

`CREATE ROLE alice WITH LOGIN PASSWORD 'secret';` &rarr; create a role with password (only has login and password)

`CREATE DATABASE pathless OWNER judege;` &rarr; owner has full control of that database

`ALTER ROLE alice CREATEDB;`&rarr; alice can create databases on this server

`ALTER USER alice PASSWORD 'asd';`

`GRANT ALL PRIVILEGES ON DATABASE appdb TO alice;` &rarr; alice can operate inside that specific database

`GRANT SELECT, INSERT ON, UPDATE ON users TO alice;` &rarr; gives access to tables, schemas, etc...

## Import and Export
`pg_dump mydb > dump.sql` &rarr; export database

`psql mydb < dump.sql` &rarr; import database

## ALTER ROLE/USER
```js
ALTER ROLE alice PASSWORD 'newpass';  // change password
ALTER ROLE alice CREATEDB;            // allow creating databases
ALTER ROLE alice SUPERUSER;           // give full admin power
ALTER ROLE alice NOSUPERUSER;         // remove admin power
```

## ALTER TABLE
```js
ALTER TABLE users ADD COLUMN email TEXT;              // add new column
ALTER TABLE users DROP COLUMN email;                  // remove column

ALTER TABLE users RENAME TO app_users;                // rename table
ALTER TABLE users RENAME COLUMN name TO full_name;    // rename column

ALTER TABLE users ALTER COLUMN age TYPE BIGINT;       // change column type

ALTER TABLE users ALTER COLUMN created_at SET DEFAULT now();  // set default value
ALTER TABLE users ALTER COLUMN created_at DROP DEFAULT;       // remove default

ALTER TABLE users ALTER COLUMN email SET NOT NULL;    // make column required
ALTER TABLE users ALTER COLUMN email DROP NOT NULL;   // allow NULL again

ALTER TABLE users
  ADD CONSTRAINT users_email_unique UNIQUE(email);    // add constraint

ALTER TABLE users
  DROP CONSTRAINT users_email_unique;                 // remove constraint
```

## ALTER Database and Schema
```js
ALTER DATABASE appdb RENAME TO appdb_v2;    // rename database
ALTER DATABASE appdb OWNER TO alice;        // change database owner
ALTER SCHEMA auth RENAME TO identity;       // rename schema
ALTER SCHEMA auth OWNER TO alice;           // change schema owner
```

## PostgeSQL Connection in Node.js
`Client` &rarr; a single thread from the Pool

`Pool` &rarr; has multiple threads that can be used by clients to perform operations

**Note** - remember to `release()` client threads after use

```js
// example in ESModules
// npm install pg

import pkg from 'pg';
const {Pool} = pkg;
const pool = new Pool ({
    user:'postgres',
    host:'localhost',
    database:'maze-game',
    password:'password',
    port:5432
});

pool.query("SELECT * FROM game;");
const con = async ()=>{
    try{
        const client = await pool.connect();
        client.query("");
        client.release();
    } catch (err) { console.error(err.message);}
}
```