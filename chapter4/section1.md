# section1

## AJAX(Asynchronous Javascript And XML)

> AJAX = Asynchronous JavaScript And XML（异步 JavaScript 及 XML）<br/>
> AJAX 是 Asynchronous JavaScript And XML 的首字母缩写。<br/>
> AJAX 并不是一种新的编程语言，而仅仅是一种新的技术，它可以创建更好、更快且交互性更强的 web 应用程序。<br/>
> AJAX 使用 JavaScript 在 web 浏览器与 web 服务器之间来发送和接收数据。<br/>
> 通过在幕后与 web 服务器交换数据，而不是每当用户作出改变时重载整个 web 页面，AJAX 技术可以使网页更迅速地响应。<br/>

#### XMLHttpRequest

###### 创建 XMLHttpRequest 对象

```javascript
function GetXmlHttpObject()
{
	var xmlHttp = null;

	try
 	{
 		// Firefox, Opera 8.0+, Safari
 		xmlHttp=new XMLHttpRequest();
 	}	
	catch (e)
 	{
 		// Internet Explorer
 		try
  		{
  			xmlHttp=new ActiveXObject("Msxml2.XMLHTTP");
  		}
 		catch (e)
  		{
  			xmlHttp=new ActiveXObject("Microsoft.XMLHTTP");
  		}
 	}
	return xmlHttp;
}
//首先创建用作 XMLHttpRequest 对象的 XMLHttp 变量。把它的值设置为 null。
//按照 web 标准创建对象 (Mozilla, Opera 以及 Safari)：XMLHttp=new XMLHttpRequest()
//按照微软的方式创建对象，在 Internet Explorer 6 及更高的版本可用：XMLHttp=new ActiveXObject("Msxml2.XMLHTTP")
//如果捕获错误，则尝试更老的方法 (Internet Explorer 5.5) ：XMLHttp=new ActiveXObject("Microsoft.XMLHTTP")
```

###### XMLHttpRequest类的使用

* .readyState属性

<table>
<tr><td>0</td><td>null</td></tr>
<tr><td>1</td><td>open</td></tr>
<tr><td>2</td><td>send</td></tr>
<tr><td>3</td><td>接收结果中</td></tr>
<tr><td>4</td><td>接受完毕</td></tr>
</table>

* .open()方法，与服务器建立连接

* .send()方法，发送请求

* .onreadyStateChange属性 = function

* .status属性

<table>
<tr><td>0</td><td>（未初始化）还没有调用send()方法</td></tr>
<tr><td>1</td><td>（载入）已调用send()方法，正在发送请求</td></tr>
<tr><td>2</td><td>（载入完成）send()方法执行完成，已经接收到全部响应内容</td></tr>
<tr><td>3</td><td>（交互）正在解析响应内容</td></tr>
<tr><td>4</td><td>（完成）响应内容解析完成，可以在客户端调用了</td></tr>
</table>

* .responseText属性 当200时结果保存在该属性内

```javascript
<script type="text/javascript">
	function change(catalog)
	{
		var httpRequest = new XMLHttpRequest();
		httpRequest.open("get", "showtable.php?catalog="+catalog);
		httpRequest.send();

		httpRequest.onreadystatechange = function()
		{
			if(httpRequest.readyState == 4 && httpRequest.status == 200)
			{
				document.getElementById("table").innerHTML = httpRequest.responseText;
			}
		}

		alert(catalog);
	}
</script>
```
