
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
    <li><a href="#array">array</a></li>
    <li><a href="#procedure">procedure</a></li>
    <li><a href="#function">function</a></li>
    <li><a href="#trigger">trigger</a></li>
    <li><a href="#backup-database">backup database</a></li>
    <li><a href="#restore-database">restore database</a></li>
  </ul>
</details>

## array
* create table
  ```
  create table table_name(
    column_1 text[],
    column_2 integer[][]
  )
  ```
* add array element
  ```
  update table_name set column_1 = array_append(column_1,value);
  ```
* remove array element
  ```
  update table_name set column_1 = array_remove(column_1,value);
  ```
* show array dimension
  ```
  select array_dims(column_name) from table_name;
  ```
* select
  ```
  select column1[index] from table_name where column2[index] = value;
  ```
* manipulating array value
  ```sh
  # insert
  insert into table_name values({value1,value2,value3},{{value1,value2,value3},{value1,value2,value3}})

  # update
  update table_name set column1 = {value1,value2,value3};

  # update with index
  update table_name set column1[index] = value;
  ```
<br />

## procedure
  ```sh
  # create
  create or replace procedure procedure_name(param1 integer, param2 integer)
  language sql
  as $$ 
  insert into table_name values(value1,value2);
  $$

  # run procedure
  call procedure_name(value1,value2);
  ```

<br />

## function
  ```sh
  # create 1
  create or replace function function_name()
  return integer as $variable_name$
  declare 
    variable_name integer;
  begin 
    select count(*) into jumlah from tb_cashier;
    return jumlah;
  end
  $variable_name$ language plpgsql;

  # create 2
  create or replace function function_name(param1 integer)
  return integer as $variable_name$
  begin 
    return param1+1;
  end
  $variable_name$ language plpgsql;

  # call function
  select function_name(param1,param2);

  # function out
  create function minmax(a integer,b integer,c integer,OUT xx integer,OUT yy integer)
  as $mm$
  begin 
    min = least(a,b,c);
    max = greatest(a,b,c);
  end
  $mm$ language plpgsql;

  # function ifelse
  do $$
  declare 
    no1 integer = 100;
    no2 integer = 90;
  begin
    if no1 > no2 then
      raise notice 'no1 greater than no2';
    elseif no1 < no2 then
      raise notice 'no2 greater than no1';
    else
      raise notice 'no1 equals no2';
    end if;
  end $$

  ```

<br />

## trigger
  ```sh
  # create
  create or replace function address_history()
  return trigger as $yes$
  begin 
    if new.alamat <> old.alamat then
      insert into tb_address_history values (old.id_user,old.address,new.address,old.username);
    endif
  return new;
  end;
  $yes$ language plpgsql; 

  # drop trigger
  drop trigger trigger_name on table_name;

  # disable trigger
  alter table table_name disable trigger trigger_name;

  # enable trigger
  alter table table_name enable trigger trigger_name;

  # renama trigger
  alter trigger trigger_name on table_name rename to new_trigger_name;
  ```

<br />

## backup database
  ```
  pg_dump -U USERNAME -h 127.0.0.1 DATABASE_NAME > /path/path/path/file_name.sql
  ```

<br />

## restore database
  ```
  psql -U USERNAME -h 127.0.0.1 DATABASE_NAME < /path/path/path/file_name.sql
  ```

<br />