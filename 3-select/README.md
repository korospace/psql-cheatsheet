
<p align="center">
    <h1 align="center">SELECT</h1>
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
    <li><a href="#select-data">select data</a></li>
    <li><a href="#where-clause">where clause</a></li>
    <li><a href="#controll-flow">controll flow</a></li>
    <li><a href="#agregat">agregat</a></li>
    <li><a href="#join">join</a></li>
    <li><a href="#union">union</a></li>
    <li><a href="#group-by">group by</a></li>
    <li><a href="#having-clause">having clause</a></li>
    <li><a href="#sub-queries">sub queries</a></li>
  </ul>
</details>

## select data
* All column. 
    ```sh
    SELECT * FROM products;
    ```
    
* specific column
    ```sh
    SELECT product_id, name FROM products;
    ```

* alias
    ```sh
    SELECT p.product_id AS 'ID Produk', 
           p.name       AS 'Produk name' 
    FROM products AS p;
    ```

* order by
    ```sh
    SELECT * FROM products 
    ORDER BY price DESC;
    ```
    NOTE:  
    - ASC is used to sort from smallest to largest
    - DESC is used to sort from largest to smallest

* limit
    ```sh
    SELECT * FROM products LIMIT {offset},{limit data};
    ```
    ```sh
    SELECT * FROM products LIMIT 2,1;
    ```
    NOTE: _sql above syntax will display product data starting from row with index 2 and display only one data_

* distinct <br/>
    _This statement is used to remove redundant data at table_
    ```sh
    SELECT DISTINCT price FROM products;
    ```
    | price(without distinct) | price(with distinct)|
    | :---: | :---: |
    | 10000 | 10000 |
    | 10000 | 12000 |
    | 10000 | 29000 |
    | 10000 |
    | 10000 |
    | 10000 |
    | 12000 |
    | 29000 |

* div <br/>
    *The DIV function is used for integer division. more details: https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html*
    ```sh
    SELECT price          AS 'without div', 
           price div 1000 AS 'with div' 
    FROM products;
    ```
    | without div | with div |
    |:---:        |:---:     |
    |       10000 |       10 |
    |       10000 |       10 |
    |       10000 |       10 |
    |       10000 |       10 |
    |       10000 |       10 |
    |       10000 |       10 |
    |       12000 |       12 |
    |       29000 |       29 |
    
* string function <br/>
    *The STRING function is used to manipulate character string effectively. more details: https://dev.mysql.com/doc/refman/8.0/en/string-functions.html*
    ```sh
    SELECT name, LOWER(name),UPPER(name),LENGTH(name) FROM products;
    ```
    | name | LOWER(name) | UPPER(name) | LENGTH(name) |
    | :---: | :---: | :---: | :---: |
    | Popcorn Creamello 150gram | popcorn creamello 150gram | POPCORN CREAMELLO 150GRAM |           25 |
    | Tricks backed chips       | tricks backed chips       | TRICKS BACKED CHIPS       |           19 |
    | Rondoleti wafer           | rondoleti wafer           | RONDOLETI WAFER           |           15 |
    | Kripik pisang sale        | kripik pisang sale        | KRIPIK PISANG SALE        |           18 |
    | Mie ayam pangsit          | mie ayam pangsit          | MIE AYAM PANGSIT          |           16 |
    | Mie ayam bakso            | mie ayam bakso            | MIE AYAM BAKSO            |           14 |
    | Mie ayam pangsit+bakso    | mie ayam pangsit+bakso    | MIE AYAM PANGSIT+BAKSO    |           22 |
    | Seblak original           | seblak original           | SEBLAK ORIGINAL           |           15 |
    
* timestamp function <br/>
    *The TIMESTAMP function is used to manipulate temporal values. more details: https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html*
    ```sh
    SELECT created_at,TIME(created_at),DAY(created_at),MONTH(created_at),YEAR(created_at) FROM products;
    ```
    | created_at | TIME(created_at) | DAY(created_at) | MONTH(created_at) | YEAR(created_at) |
    | :---: | :---: | :---: | :---: | :---: |
    | 2021-07-13 05:43:22 | 05:43:22         |              13 |                 7 |             2021 |
    | 2021-07-13 05:43:26 | 05:43:26         |              13 |                 7 |             2021 |
    | 2021-07-13 05:43:26 | 05:43:26         |              13 |                 7 |             2021 |
    | 2021-07-13 05:43:26 | 05:43:26         |              13 |                 7 |             2021 |
    | 2021-07-13 06:19:02 | 06:19:02         |              13 |                 7 |             2021 |
    | 2021-07-13 06:19:02 | 06:19:02         |              13 |                 7 |             2021 |
    | 2021-07-13 06:19:02 | 06:19:02         |              13 |                 7 |             2021 |
    | 2021-07-13 06:19:02 | 06:19:02         |              13 |                 7 |             2021 |

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