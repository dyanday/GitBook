# 常量

常量可以理解为值不可变的变量。

一个常量一旦被定义，就不能再改变或者取消定义。

## 常量的特性

1. 常量区分大小写，在定义时可以指定是否大小写敏感
2. 默认情况下，他的作用域是全局，在当前脚本任何地方都能使用
3. 新定义的常量名称不能与已定义的常量和变量名称相同
4. 在定义常量时，尽量使用大写字符便于阅读和识别
5. 常量的名称不能以$符开头，常量的值只能是特定的类型：整型、浮点型、字符串型和布尔型。

## 常量的定义

> 可以用 define() 函数来定义常量，在 PHP 5.3.0 以后，可以使用 const 关键字在类定义之外定义常量。一个常量一旦被定义，就不能再改变或者取消定义。

使用const来定义常量

用法一：const用于类成员变量，一经定义不可修改，define用于全局常量，不可用于类成员变量的定义，const可在类中使用，define不能。

用法二：const定义的常量大小写敏感，而define可通过第三个参数(为TRUE表示大小写不敏感)来指定大小写是否敏感。在运行时定义一个常量。define('TXE',100,TRUE);

用法三：const不能在条件语句中定义常量，而define函数可以。

使用define函数来定义常量。

### 语法

```php
define(string $name,mixed $value[,bool $case_insensitive=false])
```

### 参数

| 参数             | 可选 | 描述                                                        |
| :--------------- | :--- | :---------------------------------------------------------- |
| name             | 必选 | 常量的名称                                                  |
| value            | 必选 | 常量的值                                                    |
| case_insensitive | 可选 | 如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。 |

### 示例：

```php
define(URL,'http://www.baidu.com');
define(PORT,3306);

echo URL; //'http://www.baidu.com'
```

### 使用关键字 const 定义常量

```php
<?php
// 以下代码在 PHP 5.3.0 后可以正常工作
const  CONSTANT  =  'Hello World' ;

echo  CONSTANT ;
?>
```

> Note: 和使用 define() 来定义常量相反的是，使用 const 关键字定义常量必须处于最顶端的作用区域，因为用此方法是在编译时定义的。这就意味着不能在函数内，循环内以及 if 语句之内用 const 来定义常量。

## 常量是全局的

常量在定义后，默认是全局变量，可以在整个运行的脚本的任何地方使用。 以下实例演示了在函数内使用常量，即便常量定义在函数外也可以正常使用常量。

```php
define('BAIDU','http://www.baidu.com');
function abc(){
    echo BAIDU;
}
abc();
```

## 检查某个名称的常量是否存在

```
bool defined ( string $name )
```

返回值:如果该名称的常量已定义，返回 TRUE；未定义则返回 FALSE。

## 获取已定义常量

用 `get_defined_constants()` 可以获得所有已定义的常量列表。

```php
//输出所有用户定义常量
array get_defined_constants(true)['user']
```

## 预定义常量

| 常量名      | 作用                      |
| ----------- | ------------------------- |
| __FILE__    | 获取PHP程序文件名         |
| __DIR__     | PHP脚本所在的目录         |
| __LINE__    | PHP程序行数               |
| PHP_VERSION | PHP程序版本               |
| PHP_OS      | 执行PHP解析器操作系统名称 |