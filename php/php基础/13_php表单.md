# 表单

> 在 PHP 中，预定义的 $_GET 变量用于收集来自 method="get" 的表单中的值。
>
> 在 PHP 中，预定义的 $_POST 变量用于收集来自 method="post" 的表单中的值。

### $_GET 变量

预定义的 $_GET 变量用于收集来自 method="get" 的表单中的值。

从带有 GET 方法的表单发送的信息，对任何人都是可见的（会显示在浏览器的地址栏），并且对发送信息的量也有限制。

### $_POST 变量

预定义的 $_POST 变量用于收集来自 method="post" 的表单中的值。

从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制。 注释：然而，默认情况下，POST 方法的发送信息的量最大值为 8 MB（可通过设置 php.ini 文件中的 post_max_size 进行更改）。

### $_REQUEST变量

预定义的 $_REQUEST可以获取以POST方法和GET方法提交的数据，但是速度比较慢 。

### $_FILES变量

$_FILES可以获取到用户上传到后台的文件。 第一个参数是表单的 input name，第二个下标可以是 "name"、"type"、"size"、"tmp_name" 或 "error"。如下所示：

| 参数                        | 描述                                  |
| --------------------------- | ------------------------------------- |
| $_FILES["file"]["name"]     | 上传文件的名称                        |
| $_FILES["file"]["type"]     | 上传文件的类型                        |
| $_FILES["file"]["size"]     | 上传文件的大小，以字节计 1kb=1024byte |
| $_FILES["file"]["tmp_name"] | 存储在服务器的文件的临时副本的名称    |
| $_FILES["file"]["error"]    | 由文件上传导致的错误代码              |

```
if(is_uploaded_file($_FILES['f']['tmp_name'])){
    move_uploaded_file($_FILES['f']['tmp_name'],'../upload/'.$_FILES['f']['name']);
}else{
    echo "上传错误!";
}
```