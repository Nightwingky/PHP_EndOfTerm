# section1

## 文件

#### PHP 打开文件 - fopen()

* fopen() 函数用于打开文件

```php
//fopen()的第一个参数包含被打开的文件名，第二个参数规定打开文件的模式。
<?php
	$myfile = fopen("webdictionary.txt", "r") or die("Unable to open file!");
	echo fread($myfile,filesize("webdictionary.txt"));
	fclose($myfile);
?>
```

* 文件打开模式

<table>
<tr><td>模式</td><td>描述</td></tr>
<tr><td>r</td><td>打开文件为只读。文件指针在文件的开头开始。</td></tr>
<tr><td>w</td><td>打开文件为只写。删除文件的内容或创建一个新的文件，如果它不存在。文件指针在文件的开头开始。</td></tr>
<tr><td>a</td><td>打开文件为只写。文件中的现有数据会被保留。文件指针在文件结尾开始。创建新的文件，如果文件不存在。</td></tr>
<tr><td>x</td><td>创建新文件为只写。返回 FALSE 和错误，如果文件已存在。</td></tr>
<tr><td>r+</td><td>打开文件为读/写、文件指针在文件开头开始。</td></tr>
<tr><td>w+</td><td>打开文件为读/写。删除文件内容或创建新文件，如果它不存在。文件指针在文件开头开始。</td></tr>
<tr><td>a+</td><td>打开文件为读/写。文件中已有的数据会被保留。文件指针在文件结尾开始。创建新文件，如果它不存在。</td></tr>
<tr><td>x+</td><td>创建新文件为读/写。返回 FALSE 和错误，如果文件已存在。</td></tr>
</table>

#### PHP 关闭文件 - fclose()

* fclose() 函数用于关闭打开的文件。

```php
//fclose() 需要待关闭文件的名称（或者存有文件名的变量）
<?php
	$myfile = fopen("webdictionary.txt", "r");
	// some code to be executed....
	fclose($myfile);
?>
```

#### PHP 读取单行文件 - fgets()

* fgets() 函数用于从文件读取单行。

```php
<?php
	$myfile = fopen("webdictionary.txt", "r") or die("Unable to open file!");
	echo fgets($myfile);
	fclose($myfile);
?>
//调用 fgets() 函数之后，文件指针会移动到下一行。
```

#### PHP 检查 End-Of-File - feof()

* feof() 函数检查是否已到达 "end-of-file" (EOF)。<br/>
  feof() 对于遍历未知长度的数据很有用。

```php
<?php
	$myfile = fopen("webdictionary.txt", "r") or die("Unable to open file!");
	// 输出单行直到 end-of-file
	while(!feof($myfile)) 
	{
  		echo fgets($myfile) . "<br>";
	}
	fclose($myfile);
?>
```

#### PHP 写入文件 - fwrite()

* fwrite() 函数用于写入文件。

```php
//fwrite() 的第一个参数包含要写入的文件的文件名，第二个参数是被写的字符串。

<?php
	$myfile = fopen("newfile.txt", "w") or die("Unable to open file!");
	$txt = "Bill Gates\n";
	fwrite($myfile, $txt);
	$txt = "Steve Jobs\n";
	fwrite($myfile, $txt);
	fclose($myfile);
?>
```

#### 创建一个文件上传表单

```html
<html>
<body>

<form action="upload_file.php" method="post" enctype="multipart/form-data">
	<label for="file">Filename:</label>
	<input type="file" name="file" id="file" /> 
	<br />
	<input type="submit" name="submit" value="Submit" />
</form>

</body>
</html>

//<form> 标签的 enctype 属性规定了在提交表单时要使用哪种内容类型。在表单需要二进制数据时，比如文件内容，请使用 "multipart/form-data"。
//<input> 标签的 type="file" 属性规定了应该把输入作为文件来处理。举例来说，当在浏览器中预览时，会看到输入框旁边有一个浏览按钮。
```

#### 保存被上传的文件

```php
//文件上传时在服务器的 PHP 临时文件夹创建了一个被上传文件的临时副本。
//这个临时的复制文件会在脚本结束时消失。要保存被上传的文件，我们需要把它拷贝到另外的位置。
//这是一个完整的文件程序
<?php
	if($_FILES['userfile']['error'] > 0)
	{
		echo "Problem:";

		switch($_FILES['userfile']['error'])
		{
			case 1:
				echo "File exceed upload_max_filesize";
				break;
			case 2:
				echo "File exceed max_file_size";
				break;
			case 3:
				echo "File only partially uploaded";
				break;
			case 4:
				echo "No file uploaded";
				break;
			case 6:
				echo "Cannot upload file: No temp directory specified";
				break;
			case 7:
				echo "Upload failed: Cannot write to disk";
				break;
			default:
				echo "I don't know what the problem is";
				break;
		}
	}

	if($_FILES['userfile']['type'] != 'text/plain')
	{
		echo "Problem: File is not plain text";
		exit();
	}

	$upfile = "upfile/".$_FILES['userfile']['name'];

	if(is_uploaded_file($_FILES['userfile']['tmp_name']))
	{
		if(!move_uploaded_file($_FILES['userfile']['tmp_name'], $upfile))
		{
			echo "Problem: Could not move file to destination directory";
			exit();
		}
	}
	else
	{
		echo "Possible file upload attack. Filename:";
		echo $_FILES['userfile']['name'];
		exit();
	}

	echo "File uploaded successfully<br><br>";

	chmod($upfile, 777);//If your operating system is Linux, PLEASE ADD THIS LINE!!!!!

	$contents = file_get_contents($upfile);

	echo "<p>Preview</p>";
	echo $contents;
	echo "<br><br>";

	$fp = fopen("filelist.txt", 'a');
	$filename = explode(".", $_FILES['userfile']['name']);
	fwrite($fp, "\r\n");
	fwrite($fp, $filename[0]);
	fclose($fp);
?>
```
