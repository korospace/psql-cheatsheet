
<p align="center">
    <h1 align="center">SETUP PostgreSQL</h1>
    <p align="center">
        <a href="../README.md"><strong>« back to menu</strong></a>
    </p>
    <br />
    <br />
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ul>
    <li><a href="#login">login</a></li>
    <li><a href="#login">exit</a></li>
    <li><a href="#change-password">change password</a></li>
    <li><a href="#create-new-role">create new role</a></li>
  </ul>
</details>

## login 
    ```sh
    psql -h localhost -U postgres;
    ```

<br />

## exit 
    ```sh
    \q;
    ```

<br />

## change password
* count
    ```sh
    ALTER USER postgres WITH PASSWORD 'secure_password_here';
    ```

<br />

## create new role
* 1. set usename & password
    ```sh
    CREATE USER userA WITH SUPERUSER LOGIN PASSWORD 'your_password';
    ```

* 2. create database
    ```sh
    CREATE DATABASE userA;
    ```

<br />