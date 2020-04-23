# PHP函数

> PHP 的真正威力源自于它的函数。

在 PHP 中，提供了超过 1000 个内建的函数。

## 创建函数

语法：

```php
function functionName()
{
要执行的代码;
}
```

PHP 函数准则：

- 函数的名称应该提示出它的功能
- 函数名称以字母或下划线开头（不能以数字开头）
- 函数的名称不区分大小写

## PHP函数作用域

> Note: PHP 中的所有函数和类都具有全局作用域，可以定义在一个函数之内而在之外调用，反之亦然。

```php
function outer(){
    function inner(){
        echo "this is inner fn";
    }
}
inner(); // 错误 因为inner还没有创建

outer(); //调用outer()  inner() 创建

inner(); //已经创建
```

> Note: PHP 不支持函数重载，也不可能取消定义或者重定义已声明的函数。
>
> Note: 函数名是大小写无关的，不过在调用函数的时候，使用其在定义时相同的形式是个好习惯。

```php
function Login(){
    echo "is login!";
}
login();
```

## 函数参数

参数是通过调用代码将值传递给函数的局部变量。

参数是在参数列表中声明的，作为函数声明的一部分：

```php
function sum($a,$b){
    echo $a+$b;
}
sum(10,20);
```

### 通过引用传递参数

默认情况下，函数参数通过值传递（因而即使在函数内部改变参数的值，它并不会改变函数外部的值）。如果希望允许函数修改它的参数值，必须通过引用传递参数。

如果想要函数的一个参数总是通过引用传递，可以在函数定义中该参数的前面加上符号 &：

```php
function changeString(&$string){
    $string.="this is add string";
}
$str="你好";
changeString($str);
echo $str;
```

### 默认参数的值

```php
function sayName($name="input names"){
    echo $name;
}
sayName();
```

## 函数返回值

> 如需让函数返回一个值，请使用 return 语句。

值通过使用可选的返回语句返回。可以返回包括数组和对象的任意类型。返回语句会立即中止函数的运行，并且将控制权交回调用该函数的代码行。

> Note:如果省略了 return，则返回值为 NULL。

```php
function square($num)
{
    return $num * $num;
}
echo square(4);   // outputs '16'
```

## 可变函数

PHP 支持可变函数的概念。这意味着如果一个变量名后有圆括号，PHP 将寻找与变量的值同名的函数，并且尝试执行它。可变函数可以用来实现包括回调函数，函数表在内的一些用途。

```php
function foo() {
    echo "In foo()<br />\n";
}

function bar($arg = '') {
    echo "In bar(); argument was '$arg'.<br />\n";
}

// 使用 echo 的包装函数
function echoit($string)
{
    echo $string;
}

$func = 'foo';
$func();        // This calls foo()

$func = 'bar';
$func('test');  // This calls bar()

$func = 'echoit';
$func('test');  // This calls echoit()
```

### 匿名函数变量赋值示例

```php
$greet = function($name)
{
    printf("Hello %s\r\n", $name);
};

$greet('World');
$greet('PHP');
```

### 访问函数外部变量

#### global

global 关键词用于访问函数外部的全局变量。

在函数内调用函数外定义的全局变量，我们需要在函数中的变量前加上 global 关键字：

```php
$a = 100;
function num($n){
    global $a;
    echo $n + $a;
}
num(50);
```

PHP 将所有全局变量存储在一个名为`$GLOBALS[index]` 的数组中。 index 保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。

$GLOBALS — 引用全局作用域中可用的全部变量 $GLOBALS 这种全局变量用于在 PHP 脚本中的任意位置访问全局变量（从函数或方法中均可）。 PHP 在名为 $GLOBALS[index] 的数组中存储了所有全局变量。变量的名字就是数组的键。

#### 从父作用域继承变量

闭包可以从父作用域中继承变量。 任何此类变量都应该用 use 语言结构传递进去。

```php
$message = 'hello';
// 继承 $message
$example = function () use ($message) {
    var_dump($message);
};
echo $example();
```

### Static 作用域

当一个函数完成时，它的所有变量通常都会被删除。然而，有时候您希望某个局部变量不要被删除。

要做到这一点，在第一次声明变量时使用 static 关键字：

```php
function myTest()
{
    static $x=0;
    echo $x;
    $x++;
}

myTest();
myTest();
myTest();
//输出： 0 1 2
```

然后，每次调用该函数时，该变量将会保留着函数前一次被调用时的值。

> 注释：该变量仍然是函数的局部变量。

#### static用法

1. static放在函数内部修饰变量
2. static放在类里修饰属性，或方法
3. static放在类的方法里修饰变量
4. static修饰在全局作用域的变量

1.在函数执行完后，变量值仍然保存

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

2.修饰属性或方法，可以通过类名访问，如果是修饰的是类的属性，保留值

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