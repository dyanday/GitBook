# PHP面向对象

## PHP 类定义

```php
class phpClass {
    //类的变量使用 var 来声明, 变量也可以初始化值。
    var $var1;
    var $var2 = "constant string";

    function myfunc ($arg1, $arg2) {
        //变量 $this 代表自身的对象。
        $this->name = 'lili';
        [..]
    }
    [..]
}
```

## PHP 中创建对象

类创建后，我们可以使用 new 运算符来实例化该类的对象

```php
class person{
    function run(){
        echo "跑步";
    }
    function say(){
        echo "说话";
    }
}

$zhangsan = new person;
```

## 调用成员方法

```php
class person{
    function run(){
        echo "跑步";
    }
    function say(){
        echo "说话";
    }
}

$zhangsan = new person;
$zhangsan->run();
$zhangsan->say()
```

## PHP 构造函数

构造函数是一种特殊的方法。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，在创建对象的语句中与 new 运算符一起使用。

### 语法

```
function __construct( $par1, $par2 ) {
   $this->url = $par1;
   $this->title = $par2;
}
```

### 示例

```php
class person{
    function __construct($name,$age){
        $this->name = $name;
        $this->age = $age;
    }
    function run(){
        echo $this->name."喜欢跑步";
    }
    function say(){
        echo $this->name.'今年'.$this->age.'岁';
    }
}

$zhangsan = new person('张三',18);
$zhangsan->run();
$zhangsan->say()
```

## 析构函数

析构函数(destructor) 与构造函数相反，当对象结束其生命周期时（例如对象所在的函数已调用完毕），系统自动执行析构函数。

### 语法

```php
function __destruct() {

}
```

## 继承

PHP 使用关键字 extends 来继承一个类，PHP 不支持多继承，格式如下：

```php
class Child extends Parent {
   // 代码部分
}
```

## 访问控制

PHP 对属性或方法的访问控制，是通过在前面添加关键字 public，protected或 private来实现的。

public（公有）：公有的类成员可以在任何地方被访问。 protected（受保护）：受保护的类成员则可以被其自身以及其子类和父类访问。 private（私有）：私有的类成员则只能被其定义所在的类访问。

```php
class person{
    public $role ="人类";
    function __construct($name,$age){
        $this->name = $name;
        $this->age = $age;
    }
    function run(){
        echo $this->name."喜欢跑步";
        echo $this->role;
    }
    function say(){
        echo $this->name.'今年'.$this->age.'岁';
    }
    private function play(){
        echo $this->name.'玩游戏很好';
    }
}

$zhangsan = new person('张三',18);
var_dump($zhangsan);
$zhangsan->run();
$zhangsan->say();
//$zhangsan->play();//报错 方法私有
```

## 常量

可以把在类中始终保持不变的值定义为常量。在定义和使用常量的时候不需要使用 $ 符号。

常量的值必须是一个定值，不能是变量，类属性，数学运算的结果或函数调用。

```php
class Person
{
    const role = '常量值';

    function showRole() {
        echo  self::role ;
    }
}

echo Person::role;

$obj = new Person();
$obj->showRole();

echo $obj::role;
```

## Final 关键字

PHP 5 新增了一个 final 关键字。如果父类中的方法被声明为 final，则子类无法覆盖该方法。如果一个类被声明为 final，则不能被继承。

```php
class Person(){
    final public function eat() {
       echo "eat food!";
   }
}
```

## 调用父类构造方法

PHP 不会在子类的构造方法中自动的调用父类的构造方法。要执行父类的构造方法，需要在子类的构造方法中调用 `parent::__construct()`。

```php
class Parents{
    function __construct()
    {
        $this->name = "zhangsan";
    }
}

class child extends Parents{
    function __construct()
    {
        parent::__construct();
        var_dump($this);
    }

    function printName(){
        echo $this->name;
    }
}

$c = new child();
$c->printName();
```

> 当子类要使用 构造函数时，则必须在子类调用 `parent::__construct()`，否则父类的构造函数不会自动执行。

## interface

> interface是面向对象编程语言中接口操作的关键字，功能是把所需成员组合起来，用来装封一定功能的集合。它好比一个模板，在其中定义了对象必须实现的成员，通过类或结构来实现它。接口不能直接实例化。接口不能包含成员的任何代码，只定义成员本身。接口成员的具体代码由实现接口的类提供。接口使用interface关键字进行声明。

使用接口（interface），可以指定某个类必须实现哪些方法，但不需要定义这些方法的具体内容。

接口是通过 interface 关键字来定义的，就像定义一个标准的类一样，但其中定义所有的方法都是空的。

接口中定义的所有方法都必须是公有，这是接口的特性。

### 什么时候用接口？

1. 定规范，保持统一性；
2. 多个平级的类需要去实现同样的方法，只是实现方式不一样

### 接口使用规范

1. 接口不能实例化
2. 接口的属性必须是常量
3. 接口的方法必须是public【默认public】，且不能有函数体
4. 类必须实现接口的所有方法
5. 一个类可以同时实现多个接口，用逗号隔开
6. 接口可以继承接口【用的少】

```php
interface usb{
    const brand = 'siemens';    // 接口的属性必须是常量
    public function connect();  // 接口的方法必须是public【默认public】，且不能有函数体
}
// new usb();  // 接口不能实例化

// 类实现接口
class Android implements usb{
    public function connect(){  // 类必须实现接口的所有方法
        echo '实现接口的connect方法';
    }
}


interface usbA{
    public function connect();
}

interface usbB{
    public function contact();
}

// 类可以同时实现多个接口
class mi implements usbA,usbB{
    public function connect(){
        echo '实现接口的connect方法';
    }
    public function contact(){
        echo '实现接口的contact方法';
    }
}
```