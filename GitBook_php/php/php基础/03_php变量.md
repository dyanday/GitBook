# PHP变量

> 变量存储数据的容器

## 变量命名

PHP中变量名称用$和标识符表示，并遵循以下约定：

1. 在PHP中变量名是区分大小写的。
2. 变量名必须是以美元符($)开头
3. 变量名必须以字母或者下划线字符开始
4. 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
5. 变量名不能包含空格、不能以数字开头

## 声明变量

PHP 没有声明变量的命令。

变量会在首次为其赋值时被创建：

```
$x = 10;
$y = 20;
$sum = $x + $y ;
echo $sum;
```

> Note: $this 是一个特殊的变量，它不能被赋值。

## 变量操作

| 函数名         | 描述               |
| :------------- | :----------------- |
| `gettype(var)` | 检测变量类型       |
| `isset(var)`   | 检测变量是否存在   |
| `unset(var)`   | 销毁变量           |
| `empty(var)`   | 判断变量值为否为空 |

### gettype 检测变量类型

通过函数`gettype(var)`获取变量类型。

#### 语法

```
string gettype ( mixed $var )
```

#### 示例

```
$num = 100;
echo gettype($num); //integer
```

> 注意：不要使用 gettype() 来测试某种类型，因为其返回的字符串在未来的版本中可能需要改变。此外，由于包含了字符串的比较，它的运行也是较慢的。 推荐使用 is_* 函数代替。

### isset 检测变量是否存在

通过函数`isset(var)`一般用来检测变量是否设置。

#### 语法

```
bool isset ( mixed $var [, mixed $... ] )
```

#### 参数

| 参数 | 描述           |
| :--- | :------------- |
| var  | 要检查的变量。 |
| ...  | 其他变量。     |

#### 返回值

- 若变量不存在则返回 FALSE
- 若变量存在且其值为NULL，也返回 FALSE
- 若变量存在且值不为NULL，则返回 TURE 同时检查多个变量时，每个单项都符合上一条要求时才返回 TRUE，否则结果为 FALSE

#### 示例

```
$num = 100;
echo isset($num);  //存在返回 true
echo isset($link); //不存在返回 false
```

### unset 销毁变量

通过函数`unset(var)`销毁变量。

#### 语法

```
void unset ( mixed $var [, mixed $... ] )
```

#### 示例

```
$name = "allcky";
unset($name); //销毁变量
if($name){
    echo "变量存在";
}else{
    echo "变量已销毁";
}
```

### 判断值是否为空

empty() 函数 判断值为否为空

#### 语法

```
bool empty ( mixed var )
```

功能:检查一个变量是否为空

#### 规则

- 若变量不存在则返回 `TRUE` 若变量存在且其值为`""`、`0`、`"0"`、`NULL`、、`FALSE`、`array()`以及没有任何属性的对象，则返回true
- 若变量存在且值不为`""`、`0`、`"0"`、`NULL`、、`FALSE`、`array()`以及没有任何属性的对象，则返回false

## 预定义变量

### $_SERVER[]

| 变量名称                    | 说明                                |
| --------------------------- | ----------------------------------- |
| $_SERVER['SERVER_ADDR']     | 当前运行脚本所在的服务器的IP地址    |
| $_SERVER['SERVER_NAME']     | 当前运行脚本所在服务器主机的名称    |
| $_SERVER['SERVER_PORT']     | 服务器所使用的端口号                |
| $_SERVER['SCRIPT_NAME']     | 获取相对路径                        |
| $_SERVER['QUERY_STRING']    | 查询字符串                          |
| $_SERVER['REQUEST_URI']     | 路径、查询字符串                    |
| $_SERVER['REQUEST_METHOD']  | 访问页面时的请求方法。如：GET、POST |
| $_SERVER['REMOTE_ADDR']     | 正在浏览当前页面用户的IP地址        |
| $_SERVER['REMOTE_PORT']     | 用户连接到服务器时使用的端口号      |
| $_SERVER['SCRIPT_FILENAME'] | 当前执行脚本的绝对路径              |

## 可变变量

可变变量是一种独特的变量，它允许动态的改变一个变量的名称。该变量的名称由另外一个变量的值来确定。实现过程是在变量前面再多加一个$符号。

```php
$hello = "你好";
$nihao = "hello";
echo $nihao; //hello
echo $$nihao ; //你好
```

## 变量引用

PHP的引用允许你用两个变量来指向同一个内容

```php
$a="ABC";
$b =&$a;
echo $a;//这里输出:ABC
echo $b;//这里输出:ABC
$b="EFG";
echo $a;//这里$a的值变为EFG 所以输出EFG echo $b;//这里输出EFG
```

## 变量作用域

变量在使用时，要符合变量定义规则，同时变量必须在有效范围内使用，如果超出有效范围，变量也就失去意义了。

| 作用域         | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| local局部变量  | 即在函数内部定的变量，其作用域位于所在函数                   |
| global全局变量 | 即被定义在所有函数以外的变量，其作用域是整个PHP文件，但是在用户定义函数内部是不可用的，想要在用户函数内部使用全局变量要用 global关键字声明 |
| static静态变量 | 能够在函数调用结束后仍保留变量值，当再次回到其作用域时，又可以继续使用原来的值，而一般变量是在函数调用结束后，其存储的数值将被清除，所占的内存空间被释放，使用静态变量时，先要用关键字static来声明变量，需要把static放在要定义变量之前 |

### 全局作用域和局部作用域

#### 定义

- 在所有函数外部定义的变量，拥有全局作用域global；
- 在函数内部定义的变量用于局部作用域local。

#### 访问

- 全局变量可以被脚本的任何位置访问，但在函数内部访问全局变量要使用global关键字。
- 而局部变量只能在函数内部进行访问。

### 作用域

能够在函数调用结束后仍保留变量值，当再次回到其作用域时，又可以继续使用原来的值，而一般变量是在函数调用结束后，其存储的数值将被清除，所占的内存空间被释放，使用静态变量时，先要用关键字static来声明变量，需要把static放在要定义变量之前

static作用域用法如下：

1. static放在函数内部修饰变量
2. static放在类里修饰属性，或方法
3. static放在类的方法里修饰变量
4. static修饰在全局作用域的变量

#### 在函数执行完后，变量值仍然保存

如下所示：

```php
<?php
function testStatic() {
    static $val = 1;
    echo $val;
    $val++;
}
testStatic();   //output 1
testStatic();   //output 2
testStatic();   //output 3
```

#### 修饰属性或方法，可以通过类名访问，如果是修饰的是类的属性，保留值

```php
<?php
class Person {
    static $id = 0;

    function __construct() {
        self::$id++;
    }

    static function getId() {
        return self::$id;
    }
}
echo Person::$id;   //output 0
echo "<br/>";

$p1=new Person();
$p2=new Person();
$p3=new Person();

echo Person::$id;   //output 3
?>
```