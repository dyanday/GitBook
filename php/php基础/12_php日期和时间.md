# PHP命名空间

> 在PHP中，出现同名函数或是同名类是不被允许的。为防止编程人员在项目中定义的类名或函数名出现重复冲突，在PHP5.3中引入了命名空间这一概念。

### 为什么要使用命名空间？

在做项目的时候，一个文件可能会引入多个文件。如果不使用命名空间，引入的多个文件中可能存在同名的类、函数、常量，就会报错（重复定义的错误），因此PHP在5.3中引入了命名空间这个概念解决该问题。

### 命名空间解决问题

命名空间可以解决以下两类问题：

1. 用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。
2. 为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高源代码的可读性。

命名空间，即将代码划分成不同空间，不同空间的类名相互独立，互不冲突。

> 理解：
> 没有命名空间： 一个房间有2个张三，当我们叫张三，两个人都会回答。
> 有命名空间：A房间放一个张三，B房间放一个张三 ，我找A房间张三，那么只有A张三回答。B张三就知道不是他。

## 命名空间分类

命名空间分为两类：**全局空间** 和 **命名空间**

### 全局空间

全局空间：不在namespace声明的空间里面的代码都属于全局空间。

```
// new类时，可以在类前加上反斜杠\,也可以不加。
//1.php   
class Person{
    function __construct(){
            echo 'I am Person!';
        }
}
//name.php
require_once './1.php';

new Person();     //输出 I am Person!;
new \Person();    //输出 I am Person!;
```

### 命名空间

命名空间：如果需要在命名空间使用全局空间的类、函数、常量，在调用时，需要加上反斜线（代表全局空间）
如：`namespace Think`;
如：`namespace Think\Controller`; 这种反斜线分割的、层次化的，就是子命名空间。

## 定义命名空间

> 默认情况下，所有常量、类和函数名都放在全局空间下，就和PHP支持命名空间之前一样。

命名空间通过关键字namespace 来声明。如果一个文件中包含命名空间，它必须在其它所有代码之前声明命名空间。语法格式如下；

```php
<?php  
// 定义代码在 'MyProject' 命名空间中  
namespace MyProject;  

// ... 代码 ...
```

> 注意：第一个命名空间前不能有任何代码。(如有，会抛出一个fatal error)如html代码等。
>
> 注意：在声明命名空间之前唯一合法的代码是用于定义源文件编码方式的 declare 语句，如：declare(encoding='UTF-8');
>
> 注意：在命名空间下，虽然可以放置所有合法的php代码，但是受命名空间影响的仅有类、常量和函数。
>
> 通常该命名空间要遵循PSR-0命名规范（命名空间和目录结构保持一致）。

```
# 以下代码会出现语法错误：
<html>
<?php
namespace MyProject; // 命名空间前出现了“<html>” 会致命错误 -　命名空间必须是程序脚本的第一条语句
?>
```

### 示例

```php
<?PHP
namespace teacher;
class Person{
    function __construct(){
        echo "Teacher Person";
    }
}

function Teach(){
    echo "Teacher Teach";
}

const hello = "hello Teacher";


namespace student;
class Person{
    function __construct(){
        echo "Student Person";
    }
}
function Teach(){
    echo "Student Teach";
}

const hello = "hello Student";

new Person();          //echo "Student Person"   调用本空间下的 Person类
new \teacher\Person(); //echo "Teacher Person"   调用teacher下的Person类
new \student\Person(); //echo "Student Person"   调用student下的Person类
\teacher\Teach();      //echo "Teacher Teach"    调用teacher下的Teach函数
echo \teacher\hello;   //echo "hello Teacher"    访问teacher下的hello常量
echo hello;            //echo "hello Student"    访问student下的hello常量
echo \student\hello;   //echo "hello Student"    访问student下的hello常量
```

### 一个文件多个空间

一个文件中可以定义多个命名空间，定义的语法有两种，一种是简单组合语法，另一种是大括号形式语法，另外一个文件定义多个命名空间的使用一般是多个文件合并成一个文件的场景，但不到万不得已最好不要这样，因为这样增加了代码的复杂度，可读性会降低，一般情况也没有这种使用的必要。

#### 简单组合语法

```php
<?php
namespace Index;
const NUM=1;

namespace Col;
const NUM=2;
```

#### 大括号形式语法

大括号语法，一个文件多个命名空间，如果还需要写上非命名空间的代码，就只能用大括号语法，并且非命名空间代码用namespace声明一个没有名称的命名空间，再用大括号即可

```php
<?php
/*命名空间Index*/
namespace Index{
    const NUM=1;
}

/*命名空间Col*/
namespace Col{
    const NUM=2;
}

/*全局非命名空间代码*/
namespace {
    const NUM=3;
}
```

多个不同的文件可以定义同一个命名空间，也就是说同一个命名空间的内容可以分别存储到多个不同的文件中。

### 子命名空间

与目录和文件的关系很象，PHP 命名空间也允许指定层次化的命名空间的名称。因此，命名空间的名字可以使用分层次的方式定义，分隔符是`\`

```php
<?php
namespace school\teacher;
class Person(){
    function __construct(){
        echo "hello teacher";
    }
}

namespace school\student;
class Person(){
    function __construct(){
        echo "hello teacher";
    }
}

new \school\teacher\Person();   //echo "hello teacher"
new \school\student\Person();
```

### 命名空间的识别原理

没有限定名称，也就是直接使用要读取的类、常量、函数、接口名称，这种情况会读取该内容所属的命名空间的类、常量、函数、接口名称，但如果命名空间内没有相关的数据，如果是类和接口名称会返回fatal error，如果是函数和常量会自动读取全局的函数和常量，如果全局中也没有，才会报fatal error。

## 使用命名空间：别名/导入

语法：use 命名空间，可以起别名（as 别名）。

目的：在当前文件中使用其他命名空间的 类、函数、常量。（使用时，就不用加上限定名称）

```php
# index.php
<?php
namespace index;
class Teacher {
    function __construct(){
        echo "index Teacher";
    }
}
?>

#test.php
<?php
namespace  test;
include "index.php";

//给 index空间下 Teacher 类起个别名 teacher
use \index\Teacher as teacher;
new teacher();    //echo "index Teacher"
?>
```

## 参考

- 菜鸟教程 PHP 命名空间 http://www.runoob.com/php/php-namespace.html
- https://blog.csdn.net/belen_xue/article/details/78875377