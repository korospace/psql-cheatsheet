
<p align="center">
    <h1 align="center">DML</h1>
    <p align="center">
        the syntax below is used to create, update and delete data on table.<br />
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#insert-data">insert data</a></li>
    <li><a href="#update-data">update data</a></li>
    <li><a href="#delete-data">delete data</a></li>
    <li><a href="#transaction-controll-language">transaction controll language</a></li>
  </ul>
</details>

## insert data
* Single row
    ```sh
    INSERT INTO regions(region_id,region_name) 
    VALUES(5,'Indonesia');
    ```
* Multiple row
    ```sh
    INSERT INTO regions(region_id,region_name) 
    VALUES(6,'Malaysia'),
          (7,'Thailand'),
          (8,'Brunei Darusalaam');
    ```
<br />

## update data
```sh
UPDATE regions 
SET 
    region_name = 'Indonesia xx' 
WHERE 
    region_id = 5;
```
NOTE:  
- if you not use where clause sql will change all data. so be careful
<br />

## delete data
```sh
DELETE FROM regions WHERE region_id = 7;
```
NOTE:  
- if you not use where clause sql will delete all data. so be careful
<br />

## transaction controll language
| region_id | region_name |
| :---: | :---: |
| 1 | Europe|
| 2 | Americas|
| 3 | Asia|
| 4 | Middle East and Africa|

* rollback
    ```sh
    begin;

    INSERT INTO regions(region_id,region_name) 
    VALUES(5,'Indonesia');

    rollback;
    ```
    *result*
    | region_id | region_name |
    | :---: | :---: |
    | 1 | Europe|
    | 2 | Americas|
    | 3 | Asia|
    | 4 | Middle East and Africa|

* commit
    ```sh
    begin;

    INSERT INTO regions(region_id,region_name) 
    VALUES(5,'Indonesia');

    commit;
    ```
    *result*
    | region_id | region_name |
    | :---: | :---: |
    | 1 | Europe|
    | 2 | Americas|
    | 3 | Asia|
    | 4 | Middle East and Africa|
    | 5 | Indonesia|

* savepoint
    ```sh
    begin;
    savepoint first_condition;

    DELETE FROM regions WHERE region_id = 4;
    savepoint delete1;

    DELETE FROM regions WHERE region_id = 3;
    savepoint delete2;

    rollback to savepoint first_condition;
    commit;
    ```
    *result*
    | region_id | region_name |
    | :---: | :---: |
    | 1 | Europe|
    | 2 | Americas|
    | 3 | Asia|
    | 4 | Middle East and Africa|