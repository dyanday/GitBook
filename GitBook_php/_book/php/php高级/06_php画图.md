# PHP画图

> 在PHP中,有些功能是核心功能,如数组及数组函数,默认就有这些函数; 有一些功能则是扩展功能,需要引入扩展才能用,如mysql_*函数,pdo,gd

PHP 不仅限于只产生 HTML 的输出，还可以创建及操作多种不同格式的图像文件。PHP提供了一些内置的图像信息函数，也可以使用GD函数库创建新图像或处理已有的图像。目前GD2库支持GIF、JPEG、PNG和WBMP等格式。此外还支持一些FreeType（加载操作系统中的字体）、Type1等字体库。

## GD库

GD库，是php处理图形的扩展库，GD库提供了一系列用来处理图片的API，使用GD库可以处理图片，或者生成图片。

通过GD库中的函数可以完成各种点、线、几何图形、文本及颜色的操作和处理，也可以创建或读取多种格式的图像文件。

1. 新建空白画布(指定宽高)
2. 创建颜料
3. 画图形(椭圆,矩形,直线等),或写字
4. 输出/保存图形
5. 销毁画布(关闭画板)

## 使用详解

### 创建画布

用PHP的GD库处理图像时，必须对画布进行管理。创建画布就是在内存中开辟一块存储区域，以后在PHP中对图像的所有操作都是基于这个图布处理的，图布就是一个图像资源。

在PHP中，可以使用imagecreate()和imageCreateTrueColor()两个函数创建指定的画布。这两个函数的作用是一致的，都是建立一个指定大小的画布，它们的原型如下所示：

```php
# 新建一个基于调色板的图像
resource imagecreate(int $x_size,int $y_size);

# 新建一个真彩色图像
resource imagecreatetruecolor(int $x_size,int $y_size);
```

当画布创建后，返回一个图像标识符，代表了一幅宽度为$x_size和高度为$y_size的空白图像引用句柄。在后续的绘图过程中，都需要使用这个资源类型的句柄。

例如，可以通过调用imagex() 和 imagey() 两个函数获取图片的大小。

```php
$img = imgcreatetruecolor(300,200); //创建一个300*200的画布
echo imagesx($img); //输出画布宽度 300
echo imagesy($img); //输出画布高度 200
```

### 销毁画布

画布的引用句柄如果不再使用，一定要将这个资源销毁，释放内存与该图像的存储单元。

```php
# 销毁图像
bool imagedestroy(resource $image)
```

### 设置颜色

美丽的图像，离不开色彩。在PHP中设置图像中的颜色，需要调用imagecolorallocate() 函数完成。如果在图像中需要设置多种颜色，只要多次调用该函数即可。

```
int imagecolorallocate(resource $image,int $red,int $green,int $blue); //分配颜色
```

该函数会返回一个标识符，代表了由给定的RGB组成的颜色。参数是0-255的整数或十六进制的0x00 - 0xFF。

```php
$img = imagecreate(100,100);

//rgb设置颜色
$bgColor = imagecolorallocate($img,255,0,0);
$white = imagecolorallocate($img,255,255,255);

//十六进制方式
$white = imagecolorallocate($img,0xFF,0xFF,0xFF);
$black = imagecolorallocate($img,0x00,0x00,0x00);
```

对于用 `imagecreate()` 建立的图像，第一次调用 `imagecolorallocate()` 会给图像填充背景。 对于用 `imagecreatetruecolor()` 建立的图像，则需要使用别的指令如 `imagefill()` 填充背景。

### 生成图像

使用GD库中提供的函数动态绘制完成图像以后，就需要输出到浏览器或者将图像保存起来。在PHP中，可以将动态绘制完成的画布，直接生成GIF、JPEG、PNG和WBMP四种图像格式。

```
bool imagegif(resource $image[,string $filename]); //以GIF格式将图像输出
bool imagejpeg(resource $image[,string $filename[,int $quality]]); //以JPEG格式将图像输出
bool imagepng(resource $image[,string $filename]); //以PNG格式将图像输出
bool imagewbmp(resource $image[,string $filename[,int $foreground]]); //以WBMP格式将图像输出
```

当访问时则直接将原图像流输出，并在浏览器中显示动态输出的图像。但是一定要在输出之前，使用header()函数发送http头信息，来通知浏览器使用正确的MIME类型对接受的内容进行解析，让浏览器知道我们发送的是图片。

```php
$img = imagecreate(100,100);

# 发送git图片
header("Content-type:image/gif");
imagegif($img);

# 发送jpeg图片
header("Content-type:image/jpeg");
imagejpeg($img);

# 发送png图片
header("Content-type:image/png");
imagepng($img);

# 发送wbmp图片
header("Content-type:image/vnd.wap.wbmp");
imagewbmp($img);
```

## 绘制函数

### 填充区域

```php
bool imagefill( resource $image , int $x , int $y , int $color )
```

imagefill()在image图像的(x,y)处用 color颜色执行区域填充（即与 (x, y) 点颜色相同且相邻的点都会被填充）

### 画点

```php
bool imagesetpixel( resource $image , int $x , int $y , int $color )
```

### 画线

```php
bool imageline( resource $image , int $x1 , int $y1 , int $x2 , int $y2 , int $color )
```

从(x1, y1)到(x2,y2)。线的风格可以由`bool imagesetstyle( resource $image , array $style )`来控制。宽度由`bool imagesetthickness ( resource $image , int $thickness )`控制，注意这个宽度在画矩形、弧线时也生效。

### 字符

水平地画一个字符

```
bool imagechar(resource $image , int $font , int $x , int $y , string $c , int $color)
```

垂直地画一个字符

```
bool imagecharup(resource $image , int $font , int $x , int $y , string $c , int $color)
```

水平地画一行字符串

```
bool imagestring(resource $image , int $font , int $x , int $y , string $s , int $col)
```

垂直地画一行字符串

```
bool imagestringup(resource $image , int $font , int $x , int $y , string $s , int $col)
```

$font参数要注意下，要么使用内置的字体（从1到5），要么用`int imageloadfont ( string $file )`加载字体后再设置。

### 绘制形状

矩形

```
bool imagerectangle ( resource $image , int $x1 , int $y1 , int $x2 , int $y2 , int $col )
```

椭圆

```
bool imageellipse ( resource $image , int $cx , int $cy , int $w , int $h , int $color )
```

多边形

```
bool imagepolygon ( resource $image , array $points , int $num_points , int $color )
```

## 验证码

```php
<?php
class Code{
    public $width = 120; //宽度
    public $height = 60; //高度
    public $nums = 4;    //验证码数量
    public $font_file = './font/微软雅黑+Arial.ttf'; //字体位置
    public $font_size = array('min'=>20,'max'=>26);
    public $pointer_num = 200;
    private $pic = null;
    private $letter = "abcdeB6DfEg7FVBh5KLiHUT8Mg4kAl3mCa9oT1pqR0r2OstIuvPQwxyz";

    //获取图片
    private function createPic(){
        $this->pic = imagecreatetruecolor($this->width,$this->height);
    }

    //填充背景色
    private function fillBg(){
        $color = imagecolorallocate($this->pic,rand(0,127),rand(0,127),rand(0,127));
        imagefill($this->pic,0,0,$color);
    }
    //获取随机位置
    private function getPos(){
        $w = $this->width;
        $h = $this->height;
        return array('x'=>rand(0,$w),'y'=>rand(0,$h));
    }
    //填充点
    private function fillPixel(){
        for ($i=0;$i<$this->pointer_num;$i++){
            $color = imagecolorallocate($this->pic,rand(0,255),rand(0,255),rand(0,255));
            $pos = $this->getPos();
            imagesetpixel($this->pic,$pos['x'],$pos['y'],$color);
        }
    }
    //填充线条
    private function fillLine(){
        for ($i=0;$i<10;$i++){
            $color = imagecolorallocate($this->pic,rand(0,127),rand(0,127),rand(0,127));
            $p1 = $this->getPos();
            $p2 = $this->getPos();
            imageline($this->pic,$p1['x'],$p1['y'],$p2['x'],$p2['y'],$color);
        }
    }
    //填充文字
    private function fillText(){
        $len = strlen($this->letter);
        $ww = $this->width/$this->nums;
        $hh = $this->height/2;
        $fonts = array();
        for ($i=0;$i<$this->nums;$i++){
            $l = substr($this->letter,rand(0,$len),1);
            while (in_array($l,$fonts)){
                $l = substr($this->letter,rand(0,$len),1);
            }
            $fonts[] = $l;
        }
        for($i=0;$i<$this->nums;$i++){
            $font_size = rand($this->font_size['min'],$this->font_size['max']);
            $color = imagecolorallocate($this->pic,rand(127,255),rand(127,255),rand(127,255));
            imagettftext($this->pic,$font_size,rand(-15,15),$ww*$i+7,rand($hh,$hh+20),$color,$this->font_file,$fonts[$i]);
        }
    }
    //获取验证码
    public function getCode(){
        $this->createPic();
        $this->fillBg();
        $this->fillPixel();
        $this->fillLine();
        $this->fillText();
        return imagepng($this->pic);
    }
}
header('Content-Type:image/png');
$c = new Code();
$c->getCode();
```

## 水印图

## 缩略图

## 推荐

[PHP画图基础](http://blog.csdn.net/morewindows/article/details/7274870)