# PHP运算符

### 算数运算符

| 运算符 | 名称 | 例子       |
| ------ | ---- | ---------- |
| +      | 加法 | $x+$y      |
| -      | 减法 | $x-$y      |
| *      | 乘法 | $x*$y      |
| /      | 除法 | $x/$y      |
| %      | 取余 | $x%$y      |
| -      | 取反 | -$x        |
| .      | 并置 | $str1.$str |

### 赋值运算符

PHP赋值运算符用于向变量写值。

| 运算符 | 例子           | 作用 |
| ------ | -------------- | ---- |
| =      | $x = 100       | 赋值 |
| +=     | $x += 10       | 加法 |
| -=     | $x -= 10       | 减法 |
| *=     | $x *= 10       | 乘法 |
| /=     | $x /= 3        | 除法 |
| %=     | $x %= 2        | 取余 |
| .=     | $str .= "lisi" | 连接 |

### 递增/递减运算符

| 运算符 | 例子 | 作用            |
| ------ | ---- | --------------- |
| ++x    | ++$x | $x+1 然后返回$x |
| x++    | $x++ | 返回$x,$x+1     |
| --x    | --$x | $x-1 返回$x     |
| x--    | $x-- | 返回$x,$x-1     |

### 比较运算符

比较运算符返回的结果为布尔值。

| 运算符 | 例子     | 作用                          |
| ------ | -------- | ----------------------------- |
| ==     | 等于     | 比较值是否相同                |
| ===    | 恒等于   | 比较值是否相等、类型是否相同  |
| !=     | 不等于   | 值不相等                      |
| <>     | 不等于   | 值不相等                      |
| !==    | 不恒等   | 值或类型不相同                |
| >      | 大于     | $x>$y $x比$y大返回true        |
| <      | 小于     | $x<$y $x小于$y返回true        |
| >=     | 大于等于 | $x>=$y $x比$y大或相等返回true |
| <=     | 小于等于 | $x<=$y $x比$y小或相等返回true |

### 逻辑运算符

| 运算符 | 名称 | 例子      | 结果                                             |
| ------ | ---- | --------- | ------------------------------------------------ |
| and    | 与   | $x and $y | 如果 $x 和 $y 都为 true，则返回 true             |
| or     | 或   | $x or $y  | 如果 $x 和 $y 至少有一个为 true，则返回 true。   |
| xor    | 异或 | $x xor $y | 如果 $x 和 $y 有且仅有一个为 true，则返回 true。 |
| &&     | 与   | $x && $y  | 如果 $x 和 $y 都为 true，则返回 true。           |
| II     | 或   | $x II $y  | 如果 $x 和 $y 至少有一个为 true，则返回 true。   |
| !      | 非   | !$x       | 如果 $x 不为 true，则返回 true。                 |

### PHP 数组运算符

PHP 数组运算符用于比较数组：

| 运算符 | 名称   | 例子      | 结果                                                         |
| ------ | ------ | --------- | ------------------------------------------------------------ |
| +      | 联合   | $x + $y   | $x 和 $y 的联合（但不覆盖重复的键）                          |
| ==     | 相等   | $x == $y  | 如果 $x 和 $y 拥有相同的键/值对，则返回 true。               |
| ===    | 全等   | $x === $y | 如果 $x 和 $y 拥有相同的键/值对，且顺序相同类型相同，则返回 true。 |
| !=     | 不相等 | $x != $y  | 如果 $x 不等于 $y，则返回 true。                             |
| <>     | 不相等 | $x <> $y  | 如果 $x 不等于 $y，则返回 true。                             |
| !==    | 不全等 | $x !== $y | 如果 $x 与 $y 完全不同，则返回 true。                        |

### 三元运算符

```
$var = exp?x:y；
```

### 错误控制符 @

在PHP中，可以使用@运算符来抑制单个错误。例如，如果不希望PHP报告它不包括某个文件，则可以编写如下代码：

```php
@include ('config.inc.php');
```

或者如果不希望看到“除以0”错误：

```php
$x = 8;
$y = 0;
$num = @($x/$y);
```

像函数调用或数学运算一样，@符号只能处理表达式。不能在条件语句、循环语句、函数定义等之前使用@符号。 一条经验法则是，我建议将@符号用于那些执行失败时不会影响脚本整体功能的函数。