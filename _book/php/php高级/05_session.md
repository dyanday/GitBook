# session

PHP session 变量用于存储关于用户会话（session）的信息，或者更改用户会话（session）的设置。

Session 代表着服务器和客户端一次会话的过程。Session 对象存储特定用户会话所需的属性及配置信息。这样，当用户在应用程序的 Web 页之间跳转时，存储在 Session 对象中的变量将不会丢失，而是在整个用户会话中一直存在下去。当客户端关闭会话，或者 Session 超时失效时会话结束。

## 使用Session

在您把用户信息存储到 PHP session 中之前，首先必须启动会话。

```php
<?php session_start(); ?>

<html>
<body>
```

上面的代码会向服务器注册用户的会话，以便您可以开始保存用户信息，同时会为用户会话分配一个 UID。

### Session原理

当第一次访问网站时，Seesion_start()函数就会创建一个唯一的Session ID，并自动通过HTTP的响应头，将这个Session ID保存到客户端Cookie中。同时，也在服务器端创建一个以Session ID命名的文件，用于保存这个用户的会话信息。当同一个用户再次访问这个网站时，也会自动通过HTTP的请求头将Cookie中保存的Seesion ID再携带过来，这时Session_start()函数就不会再去分配一个新的Session ID，而是在服务器的硬盘中去寻找和这个Session ID同名的Session文件，将这之前为这个用户保存的会话信息读出，在当前脚本中应用，达到跟踪这个用户的目的。 Session以数组的形式使用，如：$_SESSION['session名']

```php
client———>1.request————————->server
                            2. session_start();
   |<————-3.reponse(SESSION_ID)<——–|
   |————->4.request(SESSION_ID)———>|
                            5. session_start();
   |<————-6.reponse(SESSION_ID)<———|
   |————->7.request(SESSION_ID + logout)–>|
                            8. session_destroy();
   |<————-9.reponse(删除cookie文件)<——-|
```

## 存储 Session 变量

存储和取回 session 变量的正确方法是使用 PHP $_SESSION 变量：

```php
<?php session_start() ?>

$_SESSION['username']='king';
```

注意：session_start()函数之前不能有任何输出

## 销毁 Session

```php
<?php
    session_start();  //启动会话

    isset($_SESSION['username']); //检测一个变量是否有值

    unset($_SESSION['username']); //销毁变量 username
```

可以通过session_destroy()函数在页面中提供一个“退出”按钮，通过单击销毁本次会话。

## Session生命周期

每次超过了SESSION的生存周期(session.gc_maxlifetime,默认是1440秒也就是24分钟)去访问的话,SESSION一定会被回收.