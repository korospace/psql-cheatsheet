
<p align="center">
    <h1 align="center">SELECT DATA</h1>
    <p align="center">
        the syntax below is used to read data on table.<br />
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#basic-select">basic select</a></li>
    <li><a href="#alias">alias</a></li>
    <li><a href="#arithmetic-operation">arithmetic operation</a></li>
    <li><a href="#concat-column">concat column</a></li>
    <li><a href="#redundant-data">redundant data</a></li>
    <li><a href="#date-operation">date operation</a></li>
    <li><a href="#timestamp-operation">timestamp operation</a></li>
    <li><a href="#null-and-empty-handler">NULL and EMPTY handler</a></li>
    <li><a href="#logical-operation">logical operation</a></li>
    <li><a href="#ordering-data">ordering data</a></li>
    <li><a href="#limit-and-offset">limit and offset</a></li>
    <li><a href="#single-row-funciton">single row funciton</a></li>
    <li><a href="#group-by">group by</a></li>
    <li><a href="#having-clause">having clause</a></li>
    <li><a href="#join">join</a></li>
    <li><a href="#case">case</a></li>
  </ul>
</details>

## select data
* All column. 
    ```sh
    SELECT * FROM table_name;
    ```
    
* specific column
    ```sh
    SELECT column_name,column_name FROM table_name
    ```
<br>

## alias
* alias for column
    ```sh
    SELECT column_name AS bla_bla FROM table_name;
    SELECT column_name AS "bla bla" FROM table_name;

    or

    SELECT column_name bla_bla FROM table_name;
    SELECT column_name "bla bla" FROM table_name;
    ```

* alias for table
    ```sh
    SELECT tn.column_name FROM table_name AS tn;

    or

    SELECT tn.column_name FROM table_name tn;
    ```
<br />

## arithmetic operation
* static data
    ```sh
    SELECT 
        2+2  AS penjumlahan, 
        2-1  AS pengurangan, 
        4/2  AS pembagian, 
        2*2  AS perkalian, 
        @ -5 AS real, 
        3%2  AS mod;
    ```

* dynamic data
    ```sh
    SELECT 
        salary          AS gaji, 
        salary*(30/100) AS "30% dari gaji" 
    FROM employees;
    ```
<br />

## concat column
* static data
    ```sh
    SELECT 
        first_name,
        last_name, 
        first_name ||' '|| last_name AS full_name 
    FROM employees;
    ```
<br />

## redundant data
* one column
    ```sh
    SELECT 
        distinct job_id,
        first_name
    FROM employees;
    ```

* two column or more
    ```sh
    SELECT
        distinct (department_id,salary),
        first_name
    from employees;
    ```
<br />

## date operation
* type data is string
    ```sh
    SELECT
        DATE '2017-03-28' - 2 AS lusa, 
        DATE '2017-03-28' - interval '2 hour' AS waktu, 
        DATE '2017-03-28' + 1 AS besok,
        DATE '2017-03-30' - DATE '2017-03-15' AS jumlah_hari_kerja;
    ```
    | lusa | waktu | besok | jumlah_hari_kerja |
    | :---: | :---: | :---: | :---: |
    | 2017-03-26 | 2017-03-27 22:00:00 | 2017-03-29 | 15 |

* type data is timestamp/date
    ```sh
    SELECT 
        start_date - end_date AS "lama kerja" 
    FROM job_history; 
    ```
    | lama kerja |
    | :---: |
    | -2018 days |
    | -1497 days |
    | -1234 days |
    | -1401 days |

<br />

## timestamp operation
```sh
SELECT
    TIMESTAMP '2017-03-28 18:20:00' - interval '15 hour'   AS waktu, 
    DATE      '2017-03-28'          + interval '26 day'    AS deadline, 
    TIMESTAMP '2017-03-02 00:04:30' + interval '5 minutes' AS makan_siang;
```
<br>
|  waktu        |      deadline       |     makan_siang |
| :---: | :---: | :---: |
| 2017-03-28 03:20:00 | 2017-04-23 00:00:00 | 2017-03-02 00:09:30|
<br />

## null and empty handler
```sh
SELECT 
    COALESCE(commission_pct,0), 
    salary 
FROM employees;
```
***this keyword selects records that have matching values in both tables.***
<br>

## where clause
* ( = )
    ```sh
    //type integer
    SELECT * FROM countries WHERE region_id = 2;

    //type string
    SELECT * FROM countries WHERE country_id = 'CN';
    ```
* ( != )
    ```sh
    //type integer
    SELECT * FROM countries WHERE region_id != 2;

    //type string
    SELECT * FROM countries WHERE country_id <> 'CN';
    ```
* IN
    ```sh
    SELECT * FROM countries WHERE region_id IN (1,2);
    ```
* BETWEEN
    ```sh
    SELECT 
        salary 
    FROM employees 
    WHERE salary BETWEEN 1000 AND 4000;
    ```
* IS NULL
    ```sh
    SELECT 
        first_name||' '||last_name AS employers 
    FROM employees 
    WHERE commission_pct IS NULL;
    ```
* LIKE
    ```sh
    //
    SELECT * from employees where first_name like 'A%';

    //
    SELECT * from employees where first_name like '_l%';
    ```
<br />

## logical operation
* AND
    ```sh
    SELECT first_name FROM employees WHERE department_id = 90 AND manager_id = 100;
    ```
* OR
    ```sh
    SELECT first_name FROM employees WHERE department_id = 90 OR manager_id = 100;
    ```
* COMBINATION
    ```sh
    SELECT * FROM employees WHERE (salary > 10000 OR commission_pct > 1000) AND department_id = 90;
    ```
* NOT
    ```sh
    SELECT * FROM countries WHERE region_id NOT IN (1,2);

    SELECT first_name FROM employees WHERE salary NOT BETWEEN 1000 AND 10000;

    SELECT first_name FROM employees WHERE commission_pct IS NOT NULL

    SELECT first_name FROM employees WHERE first_name NOT LIKE '%el%'
    ```
<br />

## ordering data
```sh
//ASCENDING
SELECT first_name,salary FROM employees ORDER BY salary DESC;

//DESCENDING
SELECT first_name,salary FROM employees ORDER BY (first_name,salary) ASC;
```
<br>

## limit and offset
```sh
SELECT * FROM employees LIMIT 10 OFFSET 2;
```
<br>

## single row funciton
```sh
SELECT
    employee_id                        AS kode,
    UPPER(first_name)                  AS nama_depan_kapital,
    INITCAP(last_name)                 AS nama_belakang,
    LENGTH(last_name)                  AS jumlah,
    CONACT(first_name, ' ', last_name) AS nama_lengkap
FROM employees;
```
<br>

## group by
```sh
SELECT 
    department_id      AS divisi,
    manager_id         AS manager,
    COUNT(*)           AS jumlah_karyawan,
    (SUM(salary) * 12) AS total_salary
FROM employees
GROUP BY divisi, manager
ORDER BY divisi;
```
<br>

## having clause
* having
    ```sh
    SELECT 
        manager_id,
        COUNT(*) AS jumlah_karyawan,
        SUM(salary)
    FROM employees
    GROUP BY manager_id
        HAVING SUM(salary) >= 20000
    ORDER BY manager_id;
    ```
* where and having
    ```sh
    SELECT 
        manager_id,
        COUNT(*) AS jumlah_karyawan, 
        SUM(salary)
    FROM employees 
        WHERE salary >= 10000
    GROUP BY manager_id
        HAVING SUM(salary) >= 20000
    ORDER BY manager_id;
    ```
<br>

## agregat
* count
    ```sh
    SELECT COUNT(product_id) AS 'total product' FROM products;
    ```
    | total product |
    | :---: |
    |            10 |
    
* sum
    ```sh
    SELECT SUM(quantity) AS 'summary of stock' FROM products;
    ```
    | summary of stock |
    | :---: |
    |              271 |
    
* avg
    ```sh
    SELECT AVG(price) AS 'average price' FROM products;
    ```
    | total stock |
    | :---: |
    |         271 |
    
* max value
    ```sh
    SELECT MAX(price) AS 'highest price' FROM products;
    ```
    | highest price |
    | :---: |
    |         29000 |
    
* min value
    ```sh
    SELECT MIN(price) AS 'lowest price' FROM products;
    ```
    | lowest price |
    | :---: |
    |        29000 |

<br />

## join
* natural join
    ```sh
    SELECT 
        c.country_name, 
        l.street_address 
    from countries c 
    natural join locations l;
    ```
    
* inner join
    ```sh
    SELECT 
        dep.manager_id,
        dep.department_name,
        em.first_name,
        em.salary 
    FROM departments dep 
    JOIN employees   em 
    ON(dep.manager_id = em.employee_id);

    //manual
    SELECT 
        dep.manager_id,
        dep.department_name,
        em.first_name,
        em.salary 
    FROM departments dep,employees em 
    WHERE dep.manager_id = em.employee_id;
    ```
    
* outer join
    ```sh
    //right join
    SELECT 
        dep.manager_id,
        dep.department_name,
        em.first_name,
        em.salary 
    FROM departments     dep 
    RIGHT JOIN employees em 
    ON(dep.manager_id = em.employee_id);

    //left join
    SELECT 
        dep.manager_id,
        dep.department_name,
        em.first_name,
        em.salary 
    FROM departments    dep 
    LEFT JOIN employees em 
    ON(dep.manager_id = em.employee_id);
    ```
    
* self join
    ```sh
    SELECT 
        em.employee_id,
        CONCAT(em.first_name,' ',em.last_name) as employee_name,
        man.manager_id, 
        CONCAT(man.first_name,' ',man.last_name) as manager_name 
    FROM employees      em 
    LEFT JOIN employees man 
    ON(man.employee_id = em.manager_id);
    ```
    <br />

## case
```sh
SELECT
    employee_id    AS kode_karyawan,
    commission_pct AS besar_komisi,
    CASE    
        WHEN COALESCE(commission_pct, 0) = 0 
            THEN 'Tidak memiliki komisi'
        ELSE
            CONCAT('Memiliki komisi sebesar ', commission_pct)
    end as deskripsi
FROM 
    employees;
```
<br>