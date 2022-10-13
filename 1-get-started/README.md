
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
    <li>
      <a href="#login">login</a>
    </li>
    <li>
      <a href="#shortcut">shortcut</a>
    </li>
    <li>
      <a href="#create-user">create user</a>
    </li>
    <li>
      <a href="#create-database">create database</a>
    </li>
    <li>
      <a href="#create-database">create database</a>
    </li>
    <li>
      <a href="#change-db-owner">change db owner</a>
    </li>
    <li>
      <a href="#change-user-privilege">change user privilege</a>
    </li>
    <li>
      <a href="#switch-database">switch database owner</a>
    </li>
  </ul>
</details>

## login 
  ```sh
  psql -U username -d db_name -h host -p port

  # or

  sudo -u postgres psql

  # remote database

  psql -h db_host -U db_username -d db_name -p db_port
  ```
  *default username,db_name and password is <b>postgres</b>

<br />

## shortcut
  ```
    \q	     -> quit
	\l		 -> database list
	\du		 -> user list
	\! clear   -> clear window
	\dt		 -> table list
	\d <table> -> table spesific      
  ```

<br />

## create user
  ```
  CREATE USER username WITH PASSWORD 'userpass';
  ```
<br />

## create database
  ```
  CREATE DATABASE db_name;
  ```
<br />

## change db owner
  ```
  ALTER DATABASE db_name OWNER TO username;
  ```
<br />

## switch database
  ```
  \c db_name username;
  ```
<br />

## change user privilege
  ```
  ALTER USER role_specification WITH OPTION1 OPTION2 OPTION3;
  ```
<br />