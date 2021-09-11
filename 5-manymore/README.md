
<p align="center">
    <h1 align="center">MANY MORE</h1>
    <p align="center">
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#backup-database">backup database</a></li>
    <li><a href="#restore-database">restore database</a></li>
  </ul>
</details>

## backup database
  ```
  pg_dump -U USERNAME -h 127.0.0.1 DATABASE_NAME > /path/path/path/file_name.sql
  ```
## restore database
  ```
  psql -U USERNAME -h 127.0.0.1 DATABASE_NAME < /path/path/path/file_name.sql
  ```