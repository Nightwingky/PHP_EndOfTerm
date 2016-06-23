# section1

## PHP基础

#### PHP基础知识

* phpinfo():php系统功能函数

* <?php ... ?>:php定界符

* 4种标量类型:布尔型（boolean）、整型数（integer）、浮点数（float）、字符串（string）

* 两种复合类型:数组（array）、对象（object）

* 两种特殊类型:资源（resource）、空值（NULL）

* 变量之前加 $ 

* "$string"取string变量的值，''内不支持$

* var_dump($array):输出类型+值

* 表单
```php
<form action = "a.php" method = "get">
	<input type = "test" name = "username"/>
	<input type = "password" name = "pwd"/>
	<input type = "submit" name = "submit" value = "OK"/>
</form>
```
```php
<?php
	echo "<form action = 'a.php' method = 'get'>";
	echo "<input type = 'test' name = 'username'/>";
	echo "<input type = 'password' name = 'pwd'/>";
	echo "<input type = 'submit' name = 'submit' value = 'OK'/>";
	echo "</form>";
?>
```
 * get：通过把参数数据加在提交表单的action属性所指的URL中，值和表单内每个字段一一对应，然后在URL中可以看到
 * post：通过HTTP POST机制，将表单的各个字段放置在HTTP HEADER内一起传送到action属性所指的URL地址中，用户看不到这个过程。
 * name属性：保存在哪个变量名中（显示在路径中）
 * value属性：按钮上提示信息
 * 点击submit时，网页发出请求，请求的网页取决于action = ""是谁，空白表示自己


* isset()函数是否有值
```php
if(isset($_GET["username"]))
{...}
```

* ob_start()：打开缓冲区<br/>
  ob_clean()：关闭缓冲区

* include函数<br/>
  当前目录下有一个文档a.msp/.txt
```php
include("a.msp");//引用目录下的a.php
```

* .表示字符串连接，不能用+
```php
$a = "a"."b";
echo $a;
//输出结果为"ab"
```

* ?代表值的传递，以get方式传
```php
<a href = "get.php?tag=1">a</a>
```

* @表示有错可以忽略
```php
@$_GET["keywords"];
```
