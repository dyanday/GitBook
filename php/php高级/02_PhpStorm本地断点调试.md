# PhpStorm本地断点调试

php代码在调试时，经常是print_r或者var_dump来断点，但是当项目较为复杂的情况下，这么做效率就非常低下了，断点调试就非常好的解决了这个问题。一开始可能不太适应断点调试，但是当习惯之后，越用越舒服。

在 PhpStorm 中，配合使用 Xdebug ，可以很方便的实现断点调试

### 下载 Xdebug

下载地址：https://xdebug.org/download.php，首先确定你的 PHP 版本，使用phpinfo()查看 PHP 版本信息，然后下载对应的 Xdebug 版本

### 开启 Xdebug 配置

打开 php.ini，找到 Xdebug 的配置，如果没有，请手动添加。

```php
[XDebug]
zend_extension="C:\xampp\php\ext\php_xdebug-2.3.3-5.5-vc11.dll"
xdebug.profiler_enable=1
xdebug.profiler_output_dir="C:\xampp\tmp"
xdebug.remote_enable=1
xdebug.remote_port=9000
xdebug.remote_host="localhost"
```

### 检查 Xdebug的安装情况

在 PhpStorm 中，File>Setting 打开系统设置，然后如下图进入 PHP 的编译器设置，如果能看到 Xdebug 的信息，说明安装成功：

![img](http://end.hnz.kim/amWiki/images/xdebug/jiancha.png)

在 PhpStorm 中，开启监听
![img](http://end.hnz.kim/amWiki/images/xdebug/xdebug2.png)

在 PhpStorm 中，添加断点。在浏览器访问项目网址进入调试模式：
![img](http://end.hnz.kim/amWiki/images/xdebug/xdebug.png)