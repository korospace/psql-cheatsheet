
<p align="center">
    <h1 align="center">DDL</h1>
    <p align="center">
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li>
        <a href="#schema">schema</a>
    </li>
    <li>
        <a href="#create-table">create table</a>
    </li>
    <li>
        <a href="#drop-table">drop table</a>
    </li>
    <li>
        <a href="#alter-table">alter table</a>
    </li>
    <li>
        <a href="#constraint">constraint</a>
    </li>
    <li>
        <a href="#drop-constraint">drop constraint</a>
    </li>
    <li>
        <a href="#auto-increment">auto increment</a>
    </li>
    <li>
        <a href="#unique-identifier">unique identifier</a>
    </li>
  </ul>
</details>

## schema
* create
    ```
    CREATE SCHEMA test;
    ```
* drop
    ```
    DROP SCHEMA test;
    ```
<br />

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
<br />

## drop table
```
DROP TABLE test_table;
```
<br />

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
<br />

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
    ```

* primary key
    ```sh
    # when create table 
    create table test_table (
        id                  serial                  primary key,
        first_name          character varying(60)
    );

    # after create table 
    create table test_table (
        id                  serial,
        first_name          character varying(60)
    );

    ALTER TABLE test_table ADD CONSTRAINT pk_tb PRIMARY KEY (id);
    ```

* foreign key
    ```sh
    # when create table 
    create table dompet(
		id_user integer references users(id_user) on delete cascade on update cascade,
		saldo decimal default 0
	);

    # after create table 
    ALTER TABLE wallets ADD CONSTRAINT fk_wallets_to_users FOREIGN KEY (user_id) REFERENCES users(id) ON UPDATE CASCADE ON DELETE CASCADE;

<br>

## drop constraint
```
ALTER TABLE test_table DROP CONSTRAINT ft_unique;
```

## auto increment
* using serial
    ```
    create table test_table (
        id                  serial,
        first_name          character varying(60)   not null
    );
    ```

* manual
    ```sh
    CREATE SEQUENCE IF NOT EXISTS test_id_seq 
    START WITH  1 
    INCREMENT  BY 1;

    create table test_table (
        id               integer default nextval('test_id_seq'),
        first_name       character varying(60)   not null
    );

    # if you want to remove sequence
    DROP SEQUENCE test_id_seq;
    ```

## unique identifier
```sh
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

create table test_table (
    id                  character varying(64)   default uuid_generate_v4(),
    first_name          character varying(60)   not null
);

# if you want to remove extension
DROP EXTENSION IF NOT EXISTS "uuid-ossp";
```

|                  id                  | first_name |
| :---: | :---: |
| 44a38e52-25c7-4d92-a593-498ca4bd9a2f | user 1 here |