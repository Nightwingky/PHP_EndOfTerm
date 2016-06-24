# section1

## 图像处理

#### GD库（Graphic Device）

>PHP的GD库是用来处理图形的扩展库，通过GD库提供的一系列API，可以对图像进行处理或者直接生成新的图片。
>PHP除了能进行文本处理以外，通过GD库，可以对JPG、PNG、GIF、SWF等图片进行处理。GD库常用在图片加水印，验证码生成等方面。
>PHP默认已经集成了GD库，只需要在安装的时候开启就行。

```php
header("content-type: image/png");
$img=imagecreatetruecolor(100, 100);
$red=imagecolorallocate($img, 0xFF, 0x00, 0x00);
imagefill($img, 0, 0, $red);
imagepng($img);
imagedestroy($img);
```

#### 绘制线条

```php
//新建画布，通过imagecreatetruecolor函数可以创建一个真彩色的空白图片
$img = imagecreatetruecolor(100, 100);

//通过imagecolorallocate函数分配画笔颜色，通过参数设定RGB的颜色值来确定画笔的颜色
$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);

//绘制线段函数imageline进行线条的绘制，通过指定起点跟终点来最终得到线条
imageline($img, 0, 0, 100, 100, $red);

//通过header与imagepng进行图像的输出。
header("content-type: image/png");
imagepng($img);

//可以通过imagepng函数指定文件名将绘制后的图像保存到文件中。
imagepng($img, 'img.png');

//调用imagedestroy释放该图片占用的内存。
imagedestroy($img);
```

#### 绘制文字

```php
$img = imagecreatetruecolor(100, 100);
$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);
//使用imagestring函数来进行文字的绘制
//imagestring ( resource $image , int $font , int $x , int $y , string $s , int $col )
//通过$font来设置字体的大小，x,y设置文字显示的位置，$s是要绘制的文字,$col是文字的颜色。
imagestring($img, 5, 0, 0, "Hello world", $red);

header("content-type: image/png");
imagepng($img);
imagedestroy($img);
```

#### 一个完整的图像处理程序——验证码

```php
<?php
	session_start();

	$image = imagecreatetruecolor(100, 30);
	$bgcolor = imagecolorallocate($image, 255, 255, 255);

	imagefill($image, 0, 0, $bgcolor);

	$verificationCode = '';

	for($i = 0; $i < 4; $i++)
	{
		$fontsize = 18;
		$fontcolor = imagecolorallocate($image, rand(0, 120), rand(0, 120), rand(0, 120));

		$data = 'qwertyuiopasdfghjklxcvbnmQWERTYUIPASDFGHJKLXCVBNM13456789';
		$fontcontent = substr($data, rand(0, strlen($data)), 1);
		$verificationCode .= $fontcontent;

		$x = ($i*100/4 + rand(5, 10));
		$y = rand(5, 10);

		imagestring($image, $fontsize, $x, $y, $fontcontent, $fontcolor);
	}

	$_SESSION['authcode'] = $verificationCode;

	for($i = 0; $i < rand(100, 200); $i++)
	{
		$pointcolor = imagecolorallocate($image, rand(100, 200), rand(100, 200), rand(100, 200));
		imagesetpixel($image, rand(1, 99), rand(1, 29), $pointcolor);
	}

	for($i = 0; $i < rand(10, 15); $i++)
	{
		$linecolor = imagecolorallocate($image, rand(120, 250), rand(120, 250), rand(120, 250));
		imageline($image, rand(1, 99), rand(1, 29), rand(1, 99), rand(1, 29), $linecolor);
	}

	header('content-type: image/png');
	imagepng($image);

	imagedestroy($image);
?>
```