# section1

## PHP与MySQL

#### MySQL的连接与关闭

###### mysql_connect()连接到一个 MySQL 数据库

* mysql_connect(servername,username,password);

<table>
<tr><td>参数</td><td>描述</td></tr>
<tr><td>servername</td><td>可选。规定要连接的服务器。默认是 "localhost:3306"。</td></tr>
<tr><td>username</td><td>可选。规定登录所使用的用户名。默认值是拥有服务器进程的用户的名称。</td></tr>
<tr><td>password</td><td>可选。规定登录所用的密码。默认是 ""。</td></tr>
</table>

```php
在一个变量中 ($con) 存放了在脚本中供稍后使用的连接。如果连接失败，将执行 "die" 部分：
<?php
  $con = mysql_connect("localhost","peter","abc123");
  if (!$con)
  {
    die('Could not connect: ' . mysql_error());
  }
?>
```

###### mysql_close()关闭连接

* mysql_close($con);

```php
<?php
  $con = mysql_connect("localhost","peter","abc123");
  if (!$con)
  {
    die('Could not connect: ' . mysql_error());
  }

  mysql_close($con);
?>
```

#### Mysql语句的执行

###### 选择数据库。

* mysql_select_db("my_db", $con);

###### 执行MySQL语句

* mysql_query("str", $con)

###### CREATE

```sql
//CREATE DATABASE 语句用于在 MySQL 中创建数据库。
CREATE DATABASE database_name;

//CREATE TABLE 用于在 MySQL 中创建数据库表。
CREATE TABLE table_name
(
  column_name1 data_type,
  column_name2 data_type,
  column_name3 data_type,
  .......
);
```

```php
<?php
  $con = mysql_connect("localhost","peter","abc123");
  if (!$con)
  {
    die('Could not connect: ' . mysql_error());
  }

  if (mysql_query("CREATE DATABASE my_db",$con))
  {
    echo "Database created";
  }
  else
  {
    echo "Error creating database: " . mysql_error();
  }

  mysql_close($con);
?>
```

```
<?php
  $con = mysql_connect("localhost","peter","abc123");
  if (!$con)
  {
    die('Could not connect: ' . mysql_error());
  }

  // Create database
  if (mysql_query("CREATE DATABASE my_db",$con))
  {
    echo "Database created";
  }
  else
  {
    echo "Error creating database: " . mysql_error();
  }

  // Create table in my_db database
  mysql_select_db("my_db", $con);
  $sql = "CREATE TABLE Persons 
  (
    FirstName varchar(15),
    LastName varchar(15),
    Age int
  )";
  mysql_query($sql,$con);

  mysql_close($con);
?>

