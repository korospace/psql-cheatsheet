<p align="center">
    <h1 align="center">SETUP PostgreSQL</h1>
</p>

## login 
  ```
  psql -U username -d db_name -h host -p port
  ```
  *default username,db_name and password is <b>postgres</b>

## shortcut
  ```
    \q		-> quit
	\l		-> database list
	\du		-> user list
	\! clear	-> clear window
	\dt		-> table list
  ```

## create user
  ```
  CREATE USER username WITH PASSWORD 'userpass';
  ```

## create database
  ```
  CREATE DATABASE db_name;
  ```

## change db owner
  ```
  ALTER DATABASE db_name OWNER TO username;
  ```

## switch database
  ```
  \c db_name username;
  ```
<br>
<br>
<br>

<p align="center">
    <h1 align="center">DDL</h1>
</p>

## schema
* create
    ```
    CREATE SCHEMA test;
    ```
* drop
    ```
    DROP SCHEMA test;
    ```

## create table
* public schema
    ```
    create table test_table (
        id serial primary key,
        first_name character varying(60) not null,
        birtdate date not null,
        is_active boolean default false,
        balance decimal not null default 0,
        created_datetime timestamp not null default now()
    );
    ```

* custom schema
    ```
    create table test.test_table (
        id serial primary key,
        first_name character varying(60) not null,
        birtdate date not null,
        is_active boolean default false,
        balance decimal not null default 0,
        created_datetime timestamp not null default now()
    );
    ```

## drop table
```
DROP TABLE test_table;
```

## alter table
* add column
    ```
    ALTER TABLE test_table ADD COLUMN test_column integer;
    ```
* drop column
    ```
    ALTER TABLE test_table DROP COLUMN test_column;
    ```
* change default value
    ```
    ALTER TABLE test_table ALTER COLUMN test_column SET DEFAULT 'this is default value';
    ```
* change data type
    ```sh
    # char
    ALTER TABLE test_table ALTER COLUMN test_column TYPE char(100);
    # int
    ALTER TABLE wallets    ALTER COLUMN test_column TYPE INT USING test_column::integer;
    ```
* change column name
    ```
    ALTER TABLE test_table RENAME COLUMN test_column to test_new;
    ```
* rename table
    ```
    ALTER TABLE test_table RENAME TO test_new;
    ```

## constraint
* not null constraint
    ```
    create table test_table (
        id                  serial,
        first_name          character varying(60)   not null
    );
    ```

* unique constraint
    ```sh
    # when create table 
    create table test_table (
        id                  serial,
        first_name          character varying(60)   unique,
        title               character varying(60)   unique
    );

    # after create table 
    create table test_table (
        id                  serial,
        first_name          character varying(60),
        title               character varying(60)
    );

    ALTER TABLE test_table ADD CONSTRAINT ft_unique UNIQUE (first_name,title);
    ```
* check
    ```sh
    # when create table 
    create table test_table(
        id serial,
        cost numeric check(cost > 0),
        discount numeric check(discount > 0),
        check(cost > discount)
    )

    # after create table 
    create table test_table (
        id                  serial,
        first_name          character varying(60)
    );

    ALTER TABLE test_table ADD CONSTRAINT ft_check CHECK (first_name != '');