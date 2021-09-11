
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

## where clause
* = , !=
    ```sh
    SELECT * FROM products WHERE quantity != 10;
    ```
* < , > , <= , >=
    ```sh
    SELECT * FROM products WHERE price > 10000;
    ```
* AND , OR
    ```sh
    SELECT * FROM products WHERE price < 20000 AND quantity > 10;
    ```
* ( ) operator
    ```sh
    SELECT * FROM products WHERE (price > 10000 AND quantity > 10) OR price < 29000;
    ```
* IS NULL operator
    ```sh
    SELECT * FROM products WHERE column_name IS NULL;
    ```
* BETWEEN , NOT BETWEEN
    ```sh
    SELECT * FROM products WHERE quantity NOT BETWEEN 10 AND 40;
    ```
* IN , NOT IN
    ```sh
    SELECT * FROM products WHERE price NOT IN(10000,12000);
    ```
<br />

## controll flow
* IFNULL 
    ```sh
    SELECT category_id AS 'without IFNULL', 
           IFNULL(category_id,'not found') AS 'with IFNULL'
    FROM products;
    ```
    | without IFNULL | with IFNULL |
    | :---: | :---: |
    |              1 | 1           |
    |              1 | 1           |
    |              1 | 1           |
    |              1 | 1           |
    |              2 | 2           |
    |              2 | 2           |
    |              2 | 2           |
    |              3 | 3           |
    |           NULL | not found   |
    |           NULL | not found   |
    
* IF 
    ```sh
    SELECT quantity AS 'stock',
           IF( quantity <= 10,'low stock', 
                IF( quantity <= 40 ,'ready stock', 
                    IF( quantity > 40, 'over stock','over over stock'))) 
                        AS 'stock level' 
    FROM products;
    ```
    | stock | stock level |
    | :---: | :---: |
    |    40 | ready stock |
    |    50 | over stock  |
    |    10 | low stock   |
    |    80 | over stock  |
    |    10 | low stock   |
    |    10 | low stock   |
    |    10 | low stock   |
    |    10 | low stock   |
    |    23 | ready stock |
    |    28 | ready stock |
    
* case
    ```sh
    SELECT quantity AS 'stock', 
        CASE quantity 
            WHEN 10 THEN 'low stock' 
            WHEN 23 THEN 'ready stock' 
            WHEN 28 THEN 'ready stock' 
            ELSE 'over stock' 
        END AS 'stock level' 
    FROM products;
    ```
    | stock | stock level |
    | :---: | :---: |
    |    40 | over stock  |
    |    50 | over stock  |
    |    10 | low stock   |
    |    80 | over stock  |
    |    10 | low stock   |
    |    10 | low stock   |
    |    10 | low stock   |
    |    10 | low stock   |
    |    23 | ready stock |
    |    28 | ready stock |

<br />

## group by
*   The GROUP BY statement groups rows that have the same values into summary rows
    ```sh
    SELECT price AS 'price group' , 
           COUNT(product_id) AS 'total product' 
    FROM products 
    GROUP BY price;
    ```
    | price group | total product |
    | :---: | :---: |
    |       10000 |             6 |
    |       11000 |             1 |
    |       12000 |             1 |
    |       22000 |             1 |
    |       29000 |             1 |
<br />

## having clause
*   The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.
    ```sh
    SELECT price AS 'price group' , 
           COUNT(product_id) AS total_product 
    FROM products 
    GROUP BY price
    HAVING total_product > 1;
    ```
    | price group | total product |
    | :---: | :---: |
    |       10000 |             6 |
<br />

## sub queries
*   ```sh
    SELECT name,price,category_id 
    FROM products 
    WHERE price = (
        SELECT MAX(price) 
        FROM products
    );
    ```
    | name                | price | category_id |
    | :---: | :---: | :---: |
    | Ayam bakar Bu Mirna | 30000 |        NULL |

*   ```sh
    SELECT name,price,category_id 
    FROM products 
    WHERE price = (
        SELECT MAX(price) 
        FROM products 
        JOIN categories 
        ON (products.category_id = categories.category_id)
    );
    ```
    | name            | price | category_id |
    | :---: | :---: | :---: |
    | Rondoleti wafer | 29000 |           1 |

*   ```sh
    SELECT MAX(price) 
    FROM (
        SELECT price 
        FROM products 
        JOIN categories 
        ON (products.category_id = categories.category_id)
    ) AS product_categories;
    ```
    | MAX(price) |
    | :---: |
    |      29000 |
<br />

## join
* inner join / join
    <br/>
    ***this keyword selects records that have matching values in both tables.***
    ```sh
    SELECT products.category_id   AS 'from products',
           categories.category_id AS 'from categories' 
    FROM products 
    INNER JOIN categories 
    ON (products.category_id =categories. category_id);
    ```
    | from products | from categories |
    | :---: | :---: |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C02           | C02             |
    | C02           | C02             |
    | C02           | C02             |
    | C03           | C03             |
    
* left join
    <br/>
    ***this keyword returns all records from the left table (table1), and the matching records from the right table (table2). The result is 0 records from the right side, if there is no match.***
    ```sh
    SELECT products.category_id   AS 'from products',
           categories.category_id AS 'from categories' 
    FROM products 
    LEFT JOIN categories 
    ON (products.category_id =categories. category_id);
    ```
    | from products | from categories |
    | :---: | :---: |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C02           | C02             |
    | C02           | C02             |
    | C02           | C02             |
    | C03           | C03             |
    | C099          | NULL            |
    | C099          | NULL            |
    
* right join
    <br/>
    ***THIS keyword returns all records from the right table (table2), and the matching records from the left table (table1). The result is 0 records from the left side, if there is no match.***
    ```sh
    SELECT products.category_id 
    FROM products 
    RIGHT JOIN categories 
    ON (products.category_id = categories.category_id);
    ```
    | from products | from categories |
    | :---: | :---: |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C01           | C01             |
    | C02           | C02             |
    | C02           | C02             |
    | C02           | C02             |
    | C03           | C03             |
    | NULL          | C04             |
    | NULL          | C05             |
    
* cross join
    <br/>
    ***The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by the number of rows in the second table.***
    ```sh
    SELECT products.category_id   AS 'from products',            
           categories.category_id AS 'from categories'      
    FROM products      
    CROSS JOIN categories;
    ```
    | from products | from categories |
    | :---: | :---: |
    | C01           | C01             |
    | C01           | C02             |
    | C01           | C03             |
    | C01           | C04             |
    | C01           | C05             |
    | C01           | C01             |
    | C01           | C02             |
    | C01           | C03             |
    | C01           | C04             |
    | C01           | C05             |
    | C01           | C01             |
    | C01           | C02             |
    | C01           | C03             |
    | C01           | C04             |
    | C01           | C05             |
    | C01           | C01             |
    | C01           | C02             |
    | C01           | C03             |
    | C01           | C04             |
    | C01           | C05             |
    | C02           | C01             |
    | C02           | C02             |
    | C02           | C03             |
    | C02           | C04             |
    | C02           | C05             |
    | C02           | C01             |
    | C02           | C02             |
    | C02           | C03             |
    | C02           | C04             |
    | C02           | C05             |
    | C02           | C01             |
    | C02           | C02             |
    | C02           | C03             |
    | C02           | C04             |
    | C02           | C05             |
    | C03           | C01             |
    | C03           | C02             |
    | C03           | C03             |
    | C03           | C04             |
    | C03           | C05             |
    | C099          | C01             |
    | C099          | C02             |
    | C099          | C03             |
    | C099          | C04             |
    | C099          | C05             |
    | C099          | C01             |
    | C099          | C02             |
    | C099          | C03             |
    | C099          | C04             |
    | C099          | C05             |
    <br />
## union
* union
    ```sh
    SELECT category_id FROM products UNION SELECT category_id FROM categories;
    ```
    | category_id (table products) | category_id (table categoires) | UNION |
    | :---: | :---: | :---: |
    |         C01 |         C01 |         C01 |
    |         C01 |         C02 |         C02 |
    |         C01 |         C03 |         C03 |
    |         C01 |             |        NULL |
    |         C02 |
    |         C02 |
    |         C02 |
    |         C03 |
    |        NULL |
    |        NULL |

* union all
    ```sh
    SELECT category_id FROM products UNION ALL SELECT category_id FROM categories;
    ```
    | category_id (table products) | category_id (table categoires) | UNION ALL |
    | :---: | :---: | :---: |
    |         C01 |         C01 |         C01 |
    |         C01 |         C02 |         C01 |
    |         C01 |         C03 |         C01 |
    |         C01 |             |         C01 |
    |         C02 |             |         C02 |
    |         C02 |             |         C02 |
    |         C02 |             |         C02 |
    |         C03 |             |         C03 |
    |        NULL |             |        NULL |
    |        NULL |             |        NULL |
    |             |             |         C01 |
    |             |             |         C02 |
    |             |             |         C03 |

* intersect
    <br/>
    using sub query
    ```sh
    SELECT category_id 
    FROM products 
    WHERE category_id IN (
        SELECT category_id 
        FROM categories
    );
    ```
    _or_
    <br />
    using join    
    ```sh
    SELECT products.category_id 
    FROM products 
    JOIN categories 
    ON (products.category_id = categories.category_id);
    ```
    | category_id (table products) | category_id (table categoires) | INSTERSECT |
    | :---: | :---: | :---: |
    |         C01 |         C01 |         C01 |
    |         C01 |         C02 |         C01 |
    |         C01 |         C03 |         C01 |
    |         C01 |             |         C01 |
    |         C02 |             |         C02 |
    |         C02 |             |         C02 |
    |         C02 |             |         C02 |
    |         C03 |             |         C03 |
    |        NULL |             |
    |        NULL |             |

* minus
    <br/>
    using sub query
    ```sh
    SELECT category_id 
    FROM products 
    WHERE category_id NOT IN (
        SELECT category_id 
        FROM categories
    );
    ```
    _or_
    <br />
    using left join    
    ```sh
    SELECT products.category_id 
    FROM products 
    LEFT JOIN categories 
    ON (products.category_id = categories.category_id ) 
    WHERE categories.category_id IS NULL;
    ```
    | category_id (table products) | category_id (table categoires) | INSTERSECT |
    | :---: | :---: | :---: |
    |         CO1 |         CO1 |        CO99 |
    |         CO1 |         C02 |        CO99 |
    |         CO1 |         C03 |         
    |         CO1 |             |         
    |         C02 |             |         
    |         C02 |             |         
    |         C02 |             |         
    |         C03 |             |         
    |        NULL |             |
    |        NULL |             |

    <br />