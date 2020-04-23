# 常用变量

## PHP预定义变量

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

### $_GET

### $_POST

### $_FILE

## PHP预定义常量

| 常量名      | 作用                      |
| ----------- | ------------------------- |
| __FILE__    | 获取PHP程序文件名         |
| __LINE__    | PHP程序行数               |
| __DIR__     | PHP脚本所在的目录         |
| PHP_VERSION | PHP程序版本               |
| PHP_OS      | 执行PHP解析器操作系统名称 |