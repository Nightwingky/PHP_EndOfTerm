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