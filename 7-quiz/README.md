
<p align="center">
    <h1 align="center">QUIZ</h1>
    <p align="center">
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#quiz-1">quiz 1</a></li>
  </ul>
</details>

## quiz 1
<a href="https://youtube.dimas-maryanto.com/posts/rdbms/postgresql/016-quis-section-2">questions</a>

* no.1 
    ```sh
    SELECT
        em.employee_id      AS "kode karyawan",
        dep.department_name AS "nama department",
        CONCAT(em.first_name,' ',em.last_name) AS "nama lengkap",
        TO_CHAR(em.salary,'FM999,999,999')     AS "gaji perbulan",
        TO_CHAR(em.salary+(em.salary*COALESCE(em.commission_pct, 0)),'FM999,999,999')  AS "gaji terima",
        CASE    
            WHEN COALESCE(em.commission_pct, 0) = 0 
                THEN 'Tidak memiliki komisi'
            ELSE
                TO_CHAR(em.salary*em.commission_pct,'FM999,999,999')
        end AS komisi
    FROM employees em JOIN departments dep ON(em.department_id = dep.department_id);
    ```

* no.2
    ```sh
    SELECT
        em.employee_id      AS "kode karyawan",
        CONCAT(em.first_name,' ',em.last_name)  AS "nama karyawan",
        dep.department_name AS "nama bagian",
        CASE    
            WHEN COALESCE(em.manager_id, 0) = 0 
                THEN 'Tidak memiliki manager'
            ELSE
                CONCAT(em2.first_name,' ',em2.last_name)
        end AS manager,
        j.job_title  AS "nama jabatan"
    FROM 
    employees em JOIN jobs j    ON(em.job_id = j.job_id)
        JOIN departments dep    ON(em.department_id = dep.department_id)
        LEFT JOIN employees em2 ON(em.manager_id = em2.employee_id);
    ```

* no.3
    ```sh
    SELECT
        dep.department_id   AS "dep ID",
        dep.department_name AS "dep NAME",
        TO_CHAR(SUM(em.salary),'FM999,999,999') AS "TOTAL GAJI"
    FROM 
        employees em JOIN departments dep ON(em.department_id = dep.department_id)
    GROUP BY "dep ID","dep NAME"
    ORDER BY SUM(em.salary) DESC;
    ```

* no.4
    ```sh
    SELECT
        TO_CHAR(salary*12,'FM999,999,999') AS "GAJI SETAHUN",
        COUNT(employee_id)  AS "JUMLAH KARYAWAN"
    FROM employees
    WHERE   
        commission_pct IS NOT NULL
    GROUP BY salary
    ORDER BY salary DESC;
    ```

* no.5
    ```sh
    SELECT
        em.employee_id      AS "kode karyawan",
        CONCAT(em.first_name,' ',em.last_name)  AS "nama karyawan",
        TO_CHAR(em.salary,'FM999,999,999') AS "gaji",
        j.job_title AS "nama jabatan",
        em.email
    FROM employees em JOIN jobs j ON(em.job_id = j.job_id)
    WHERE
        em.salary >= (
            SELECT 
                MAX(em2.salary) 
            FROM employees em2
            WHERE 
                em2.job_id = 'IT_PROG'
        )
    ORDER BY em.salary DESC;
    ```
<br>
