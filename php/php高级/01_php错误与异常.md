# 错误处理与异常处理

> 任何程序员在开发时都可能遇到过一些失误，或其他原因造成错误的发生。

我们在开发过程中，经常会遇到各种各样的错误，这些错误都是我们需要处理的问题，程序必须在任何情况下都要保证正常运行。

我们经常遇到的是这两种类型的错误：

- 错误
- 异常

这两种不是同一个概念。

## 错误处理

> 一般情况我们把会影响到我们程序正常运行的情况叫做错误。

错误是属于php程序自身的问题，一般是由非法的语法，环境问题导致的，使得编译器无法通过检查，甚至无法运行的情况。平时遇到的warning、notice都是错误，只是级别不同而已。

错误的类型：

1. 语法错误 (少写了; , 关键词书写错误 , 丢失了某个括号等等)
2. 环境错误 (数据库连接失败,PHP语法不解析,打开文件失败了等等)
3. 逻辑错误 (一个功能开发结束，并且正常运行，但是结果不符合预期)

### 错误级别

| 级别常量          | 错误报告描述                                 |
| :---------------- | :------------------------------------------- |
| E_ERROR           | 致命的运行时错误（它会阻止脚本的执行）       |
| E_WARNING         | 运行时警告（非致命的错误）                   |
| E_PARSE           | 从语法中解析错误                             |
| E_NOTICE          | 运行时注意消息（可能是或者可能不是一个问题） |
| E_CORE_ERROR      | 类似E_ERROR，但不包括PHP核心造成的错误       |
| E_CORE_WARNING    | 类似E_WARNING，但不包括PHP核心错误警告       |
| E_COMPILE_ERROR   | 致命的编译时错误                             |
| E_COMPILE_WARNING | 致命的编译时警告                             |
| E_USER_ERROR      | 用户导致的错误消息                           |
| E_USER_WARNING    | 用户导致的警告                               |
| E_USER_NOTICE     | 用户导致的注意消息                           |
| E_ALL             | 所有的错误、警告和注意                       |
| E_STRICT          | 关于PHP版本移植的兼容性和互操作性建议        |

### PHP常见错误

1. Depracated最低级别的错误 （deprecated不建议，不推荐，如老版本的正则ereg()函数换掉即可，并不影响PHP的执行）
2. Notice通知级别的错误（语法不恰当导致的，不影响PHP的正常运行，如打印一个未定义的变量，所以我们一开始就要养成良好的书写规范）
3. Warning警告级别的错误（必须修改代码）
4. Fatal error致命级别的错误，程序会停止
5. Parse error语法解析错误，在代码运行前检查，将无法执行代码
6. E*USER*相关的错误 由用户定义的错误，手动抛出错误时会用到

#### PHP最低级别的错误—Deprecated

Deprecated使用了不推荐不建议的操作。 示例：

```php
if(ereg('hnz','my name is hnz!',$name)){
    var_dump($name);
}else{
    var_dump('nothing find!');
}

# Deprecated: Function ereg() is deprecated in /Users/houningzhou/www/studyphp/Error/2.Deprecated.php on line 3
```

#### PHP通知级别的错误—Notice

通知级别的错误—Notice，不会终止程序执行。 示例：

```php
echo $username; //变量未定义
echo '程序继续执行';  //程序继续执行

# Notice: Undefined variable: user in /Users/houningzhou/www/studyphp/Error/1.error.php on line 3
```

#### PHP警告级别的错误—Warning

警告级别的错误—Warning，不会终止程序执行。 示例：

```php
settype($user,'abc');
echo '程序继续执行';  //程序继续执行

# Warning: settype(): Invalid type in /Users/houningzhou/www/studyphp/Error/4.Warning.php on line 2
```

#### PHP致命级别的错误—Fatal (会终止程序执行)

致命级别的错误—Fatal ，会终止程序执行； 示例：

```php
echo md6('12345');
echo '程序继续执行';  //未执行

# Fatal error: Call to undefined function md6() in /Users/houningzhou/www/studyphp/Error/5.Fatal.php on line 2
```

#### PHP语法解析错误—Parse

PHP语法解析错误—Parse，语法错误最常见，并且最容易修复。最高级别错误，程序不运行；

例如，遗漏了一个分号，就会显示错误信息。这类错误会阻止脚本执行。通常发生在程序开发时，可以通过错误报告进行修复，再重新运行。

示例：

```php
echo md6('123');
echo "程序继续执行";

echo '123'    //没有加分号

# Parse error: syntax error, unexpected end of file, expecting ',' or ';' in /Users/houningzhou/www/studyphp/Error/5.Fatal.php on line 5
```

#### E*USER*相关错误 (用户定义的错误)

### PHP如何开启错误配置选项

- 通过php.ini配置文件设置
- 通过error_reporting()函数动态设置
- 运行时设置配置选项的值

#### 通过php.ini配置文件设置

我们可以通过php配置文件(php.ini)设置错误配置。

| 选项            | 描述               |
| :-------------- | :----------------- |
| error_reporting | 设置错误报告的级别 |
| display_error   | 是否显示错误       |

```
error_reporting = E_ALL & ~E_NOTICE # 显示所有但不显示提醒错误
error_reporting = E_ALL & ~E_NOTICE                    # 显示所有但不显示通知错误
error_reporting = E_ALL & ~E_DEPRECATED & ~E_NOTICE  # 显示所有但不显示通知错误、不推荐错误
```

#### 通过error_reporting()函数动态设置

```
error_reporting()                # 专业php错误处理设置函数，动态设置错误级别
error_reporting(0)               # 不显示所有错误，但是解析parse语法错误会显示
error_reporting(-1)              # 显示所有错误
Error_reporting(E_ALL&~E_WARING) # 除了警告错误以外的错误级别都报告
```

#### 运行时设置配置选项的值

```
string ini_set ( string $varname , string $newvalue )
```

设置指定配置选项的值。这个选项会在脚本运行时保持新的值，并在脚本结束时恢复。

```php
ini_set(error_reporting,0)
ini_set(error_reporting,-1)
ini_set(error_reporting,E_ALL)
ini_set(display_errors,0)
ini_set(display_errors,OFF/0)
error_reporting(-1);
```

### trigger_error 手动抛出自定义错误信息

```
bool trigger_error ( string $error_msg [, int $error_type = E_USER_NOTICE ] )
```

示例：

```php
if(!(is_numeric($num1)&&is_numeric($num2))){
    trigger_error('num1与num2必须为合法数值',E_USER_NOTICE);
}
```

错误级别：

```
E_USER_NOTICE  # 通知级别(继续执行)
E_USER_WARNING # 警告错误(继续执行)
E_USER_ERROR   # 致命错误(程序终止执行)
```

### 处理PHP中的错误

如果用户希望在PHP脚本中，遇到上表中的某个级别的错误时，将错误消息报告给用户。则必须在配置文件php.ini中，将display_errors指令的值设置为On，开启PHP输出错误报告的功能。

项目上线后，当用户在访问时，看到显示的这些消息不仅会感到迷惑，而且还可能会过多地泄露有关服务器的信息，使服务器变得很不安全。 因此：

- 项目开发或测试期间启用此指令，可以根据不同的错误报告更好的调试程序
- 项目上线后，出于安全性和美感的目的，错误报告要将其关闭

对于开发者来说，一旦某个产品上线使用，应该立即将display_errors选项关闭，以免因为这些错误所透露的路径、数据库连接、数据表等信息而遭到黑客攻击。但是，任何一个产品上线使用后，都难免会有错误出现，那么如何记录一些对开发者有用的错误报告呢？我们可以在单独的文本文件中将错误报告作为日志记录。错误日志的记录，可以帮助开发人员或者管理人员查看系统是否存在问题。

- 将错误日志保存在指定文件中
- 将错误日志保存在系统日志中
- 将错误日志发送到邮件

#### 将错误日志保存在指定文件中

我们可以通过php配置文件(php.ini)设置记录错误配置。

| 选项               | 描述                               |
| :----------------- | :--------------------------------- |
| log_errors         | 设置是否将产生错误信息记录到日志中 |
| error_log          | 设置脚本错误将记录到的文件         |
| log_errors_max_len | 设置log_errors的最大字节数         |

```php
# php.ini
log_errors=On
error_log=G:\logs\error_log.log
```

动态设置：

```php
ini_set('display_errors','off') # 不显示错误给用户
ini_set('log_errors','on');     # 产生错误信息记录到日志中
ini_set("error_log","c:\error.log");       
error_reporting(-1); # 显示所有错误
```

#### 将错误日志保存在系统日志中

动态设置：

```php
error_reporting(-1);            # 显示所有错误
ini_set('display_errors','off');# 不显示错误给用户
ini_set('log_errors','on');     # 产生错误信息记录到日志中
ini_set("error_log", 'syslog');
```

#### 将错误日志发送到邮件

需要配置邮箱客户端发送

```php
error_reporting(-1);            # 显示所有错误
ini_set('display_errors','off') # 不显示错误给用户
ini_set('log_errors','on');
if(err){
    error_log("this is a errormsg",1,xxxxx@qq.com);
}
```

### 自定义错误处理

Set_error_handler() 函数：设置一个用户定义的错误处理函数

> 当我们使用Set_error_handler，PHP错误处理将不会起作用。

按照需求自定义错误处理形式，

- 创建错误处理函数
- 设置不同级别调用函数
- Set_error_handler() 函数指定接管错误处理函数

- https://segmentfault.com/a/1190000014254189

## 异常处理

异常（Exception）用于在指定的错误发生时改变脚本的正常流程。

异常的基本语法结构

自定一个异常类 自定义异常处理器 如何像处理异常一样处理错误 发生错误的时候将用户重定向到另一个页面

### 什么是异常？

异常：一般是业务逻辑上出现的不合预期、与正常流程不同的状况。

异常是程序正常秩序过程中出现的不正常的情况。例如：人在生长过程中，是个正常的执行过程，但是在成长过程中经常生病，这就是异常。为了避免这种不正常的情况，我们会采取一系列措施，比如：锻炼身体，吃新鲜干净的食物，营养搭配合理，以增强我们的体质，提高抗病能力。 程序中我们为了提高它运行时的健壮性，我们也得采取一些错误。

生活中的异常：

1. 早晨开门钥匙断了，我们不能不开门呀，我们可以找到备用钥匙或者开另外一个门 来处理这个问题。
2. 早晨开车上班，在行驶的过程中爆胎了，我们还要继续想办法上班，叫拖车去修理或自己更换备胎，然后去上班。

异常，不是为了发生问题了给用户一个提示，而是发生问题我们通过另外一种方案去解决。

```php
# 正常
echo '早晨起床';

echo '开车上班';

echo '到公司，开始工作';

# 异常
echo '早晨起床';

try{
    echo '开车上班';
    //抛出异常 ,throw 之后代码不再执行 ,跳转到catch继续执行
    throw new Exception("车胎爆了！");

    echo '路况很好！';
}catch(Exception $e){
    echo $e->getMessage();
    echo '更换备胎，继续开车上班';
}

echo '到公司，开始工作';
```

语法：

```php
try{          
    # 需要进行异常处理的代码段
    throw 语句抛出异常；
}catch(Exception $e){ //捕获异常
    ...
}
```

### PHP异常特点

- PHP不会主动捕获异常，需要程序中主动抛出 （throw）异常，才能捕获。
- throw会自动向上抛出
- throw之后的语句不会执行
- try后必须有catch，否则解析错误Parse error

### PHP异常处理很鸡肋？

在PHP中，因为在其他语言中就不能这样下结论了，也就是说异常和错误的说法在不同的语言有不同的说法。在PHP中任何自身的错误或者是非正常的代码都会当做错误对待，并不会以异常的形式抛出，但是也有一些情况会当做异常和错误同时抛出(据说是，我没有找到合适的例子)。也就是说，你想在数据库连接失败的时候自动捕获异常是行不通的，因为这就不是异常，是错误。但是在java中就不一样了，他会把很多和预期不一致的行为当做异常来进行捕获。

在上面的分析中我们可以看出，PHP并不能主动的抛出异常，但是你可以手动抛出异常，这就很无语了，如果你知道哪里会出问题，你添加if else解决不就行了吗，为啥还要手动抛出异常，既然能手动抛出就证明这个不是异常，而是意料之中。以我的理解，这就是PHP异常处理鸡肋的地方（不一定对啊）。所以PHP的异常机制不是那么的完美，但是使用过框架的同学都知道有这个情况：你在框架中直接写开头那段php“自动”捕获异常的代码是可以的，这是为什么？看过源码的同学都知道框架中都会涉及三个函数：register_shutdown_function，set_error_handler，set_exception_handler后面我会重点讲解着三个黑科技，通过这几个函数我们可以实现PHP假自动捕获异常和错误。

- https://blog.csdn.net/weixin_30832405/article/details/95169428