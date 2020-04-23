# 数组

数组是一个能在单个变量中存储多个值的特殊变量。

超市： 储物柜 通过编号 找到自己的物品。

## 创建数组

在 PHP 中，array() 函数用于创建数组：

```
array();
```

在 PHP 中，有三种类型的数组：

- 数值数组 - 带有数字 ID 键的数组
- 关联数组 - 带有指定的键的数组，每个键关联一个值
- 多维数组 - 包含一个或多个数组的数组

## 索引数组

这里有两种创建索引数组的方法： 自动分配 ID 键（ID 键总是从 0 开始）：

```
$cars=array("Volvo","BMW","Toyota");
```

人工分配 ID 键：

```php
$cars[0]="Volvo";
$cars[1]="BMW";
$cars[2]="Toyota";
```

### 获取数组的长度 - count() 函数

count() 函数用于返回数组的长度（元素的数量）

```php
$arr = array(1,32,4,56);
echo count($arr);
```

### 遍历索引数组

```php
<?php
$cars=array("Volvo","BMW","Toyota");
$arrlength=count($cars);

for($x=0;$x<$arrlength;$x++)
{
echo $cars[$x];
echo "<br>";
}
?>
```

## PHP 关联数组

关联数组是使用您分配给数组的指定的键的数组。 这里有两种创建关联数组的方法：

```
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
```

or:

```php
$age['Peter']="35";
$age['Ben']="37";
$age['Joe']="43";
```

### 遍历关联数组

```php
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");

foreach($age as $x=>$x_value)
{
echo "Key=" . $x . ", Value=" . $x_value;
echo "<br>";
}
?>
```

## 数组排序

数组中的元素可以按字母或数字顺序进行降序或升序排列。

### 数组排序函数

| 函数     | 描述                                 |
| -------- | ------------------------------------ |
| sort()   | 对数组进行升序排列                   |
| rsort()  | 对数组进行降序排列                   |
| asort()  | 根据关联数组的值，对数组进行升序排列 |
| ksort()  | 根据关联数组的键，对数组进行升序排列 |
| arsort() | 根据关联数组的值，对数组进行降序排列 |
| krsort() | 根据关联数组的键，对数组进行降序排列 |

```php
//对数组进行升序排列
$arr =array(10,33,23,1,32,55,43,76,87,5,77);
sort($arr);
var_dump($arr);
//对数组进行降序排列
rsort($arr);
print_r($arr);
echo "<hr>";

//对数组进行升序排列
$arr2 = array('hello','kimi','lucy','linda','aiq');
sort($arr2);
var_dump($arr2);

echo "<hr>";
//对数组的值进行升序排列
$ages  = array('li'=>23,'zhang'=>22,'king'=>25);
asort($ages);
var_dump($ages);

echo "<hr>";
//对数组的键进行升序排列
$ages  = array('li'=>23,'zhang'=>22,'king'=>25);
ksort($ages);
var_dump($ages);

echo "<hr>";
//对数组进行的值降序排列
$ages  = array('li'=>23,'zhang'=>22,'king'=>25);
arsort($ages);
var_dump($ages);

echo "<hr>";
//对数组的键进行降序排列
$ages  = array('li'=>23,'zhang'=>22,'king'=>25);
krsort($ages);
var_dump($ages);
```