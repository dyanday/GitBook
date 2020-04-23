# 流程控制

## 选择结构

> 条件语句用于根据不同条件执行不同动作。

### If...Else 语句

在 PHP 中，提供了下列条件语句：

- if 语句 - 在条件成立时执行代码
- if...else 语句 - 在条件成立时执行一块代码，条件不成立时执行另一块代码
- if...else if....else 语句 - 在若干条件之一成立时执行一个代码块
- switch 语句 - 在若干条件之一成立时执行一个代码块

#### if 语句

if 语句用于仅当指定条件成立时执行代码。 语法

```php
if (条件)
{
    条件成立时要执行的代码;
}
```

#### if...else 语句

在条件成立时执行一块代码，条件不成立时执行另一块代码，请使用 if....else 语句。 语法

```php
if (条件)
{
条件成立时执行的代码;
}
else
{
条件不成立时执行的代码;
}
```

#### if...else if....else 语句

在若干条件之一成立时执行一个代码块，请使用 if....else if...else 语句。. 语法

```php
if (条件)
{
if 条件成立时执行的代码;
}
else if (条件)
{
elseif 条件成立时执行的代码;
}
else
{
条件不成立时执行的代码;
}
```

### Switch 语句

如果您希望有选择地执行若干代码块之一，请使用 switch 语句。

```php
语法
switch (n)
{
case label1:
    如果 n=label1，此处代码将执行;
    break;
case label2:
    如果 n=label2，此处代码将执行;
    break;
default:
    如果 n 既不等于 label1 也不等于 label2，此处代码将执行;
}
```

## 循环

### For 循环

> 循环执行代码块指定的次数，或者当指定的条件为真时循环执行代码块。

for循环用于预先知道脚本要运行的次数。 语法

```php
for (初始值; 条件; 增量)
{
要执行的代码;
}
```

示例

```php
<html>
<body>

<?php
for ($i=1; $i<=5; $i++)
{
echo "The number is " . $i . "<br>";
}
?>

</body>
</html>
```

### foreach 循环

foreach 循环用于遍历数组。

```php
foreach ($array as $value)
{
要执行代码;
}
foreach ($array as $key=>$value)
{
要执行代码;
}
```

### While 循环

while 循环将重复执行代码块，直到指定的条件不成立。

```php
while (条件)
{
要执行的代码;
}
```

### do...while 语句

do...while 语句会至少执行一次代码，然后检查条件，只要条件成立，就会重复进行循环。 语法

```php
do
{
要执行的代码;
}
while (条件);
```