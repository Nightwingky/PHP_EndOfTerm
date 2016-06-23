# section1

## Cookie与Session

#### 1、Cookie

> cookie 常用于识别用户。cookie 是服务器留在用户计算机中的小文件。每当相同的计算机通过浏览器请求页面时，它同时会发送 cookie。通过 PHP，您能够创建并取回 cookie 的值。

* 发送Cookie信息

```php
//使用setcookie()函数可以向客户端发送一个Cookie信息：
setcookie(name, value, expire, path, domain, secure);

//创建名为 "user" 的 cookie，把为它赋值 "Alex Porter"。我们也规定了此 cookie 在一小时后过期
setcookie("user", "Alex Porter", time()+3600);
```

<table>
<tr><th>参数</th><th>描述</th></tr>
<tr><td>name</td><td>必需,规定 cookie 的名称</td></tr>
<tr><td>value</td><td>必需,规定 cookie 的值</td></tr>
<tr><td>expire</td><td>可选,规定 cookie 的有效期</td></tr>
<tr><td>path</td><td>可选,规定 cookie 的服务器路径</td></tr>
<tr><td>domain</td><td>可选,规定 cookie 的域名</td></tr>
<tr><td>secure</td><td>可选,规定是否通过安全的 HTTPS 连接来传输 cookie</td></tr>
</table>

* 读取Cookie信息<br/>
   $_COOKIE 变量用于取回 cookie 的值。

```php
if (isset($_COOKIE["user"]))
{
	echo "Welcome " . $_COOKIE["user"] . "!<br />";
}
else
{
	echo "Welcome guest!<br />";
}
```

* 删除 cookie<br/>
   当删除 cookie 时，您应当使过期日期变更为过去的时间点。

```php
// set the expiration date to one hour ago
setcookie("user", "", time()-3600);
```

#### 2、Session

> PHP session 变量用于存储有关用户会话的信息，或更改用户会话的设置。Session 变量保存的信息是单一用户的，并且可供应用程序中的所有页面使用。

* 开始 PHP Session<br/>
  在您把用户信息存储到 PHP session 中之前，首先必须启动会话。

```php
//session_start() 函数必须位于 <html> 标签之前
<?php session_start(); ?>
<html>
<body>

</body>
</html>
//上面的代码会向服务器注册用户的会话，以便您可以开始保存用户信息，同时会为用户会话分配一个 UID。
```

* 存储 Session 变量<br/>
  存储和取回 session 变量的正确方法是使用 PHP $_SESSION 变量：

```php
<?php
	session_start();
	// store session data
	$_SESSION['views']=1;
?>

<html>
<body>

<?php
	//retrieve session data
	echo "Pageviews=". $_SESSION['views'];
?>

</body>
</html>
```

```php
//创建一个简单的 page-view 计数器。isset() 函数检测是否已设置 "views" 变量。如果已设置 "views" 变量，我们累加计数器。如果 "views" 不存在，则我们创建 "views" 变量，并把它设置为1
<?php
	session_start();

	if(isset($_SESSION['views']))
	{
		$_SESSION['views']=$_SESSION['views']+1;
	}
	else
	{
		$_SESSION['views']=1;
		echo "Views=". $_SESSION['views'];
	}
?>
```

* 终结 Session<br/>
  可以使用 unset() 或 session_destroy() 函数。

```php
//unset() 函数用于释放指定的 session 变量：
<?php
	unset($_SESSION['views']);
?>
//也可以通过 session_destroy() 函数彻底终结 session：
<?php
	session_destroy();
?>
//session_destroy() 将重置 session，您将失去所有已存储的 session 数据。
```
