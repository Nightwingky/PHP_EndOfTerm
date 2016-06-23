# section1

## 数组

* 可保存相同或不同类型的数据，并把一组值映射为键

<table>
	<tr>
		<th align = "center">key</th>
		<th align = "center">value</th>
	</tr>
</table>

#### 1、创建数组

```php
$array1 = array(0=>6, 2=>6.66e2, "str"=>"string");

$array2[0] = 6;
$array2["str"] = "string";
```

#### 2、foreach()遍历数组

```php
foreach($array1 as $value)
{
	echo $value;
}

foreach($array2 as $key => $value)
{
	echo "$key => $value";
}
```

#### 3、多维数组
```php
<?php
$bc["economy"]=array(
		array("name"=>"小众行为学","author"=>"詹姆斯.哈金","price"=>29),
		array("name"=>"经济学就这么有趣","author"=>"梁小民","price"=>24),
		array("name"=>"屌丝经济学","author"=>"周志","price"=>23),
		array("name"=>"麻辣经济学","author"=>"王兴康","price"=>13)
		);

$bc["IT"]=array(
		array("name"=>"细说php","author"=>"高洛峰","price"=>92),
		array("name"=>"Photoshop入门宝典","author"=>"李金明","price"=>69),
		array("name"=>"ui设计经典","author"=>"Susan","price"=>34),
		array("name"=>"hadoop权威指南","author"=>"杨冬青","price"=>74)
		);
?>
```
