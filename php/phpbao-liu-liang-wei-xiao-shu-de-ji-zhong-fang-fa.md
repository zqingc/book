PHP保留两位小数的几种方法

```php
    $num = 10.4567;
     
    //第一种：利用round()对浮点数进行四舍五入
    echo round($num,2); //10.46
     
    //第二种：利用sprintf格式化字符串
    $format_num = sprintf("%.2f",$num);
    echo $format_num; //10.46
    echo sprintf("%.2f",substr(sprintf("%.3f", $num), 0, -2));  //10.45

    //第三种：利用千位分组来格式化数字的函数number_format()
    echo number_format($num, 2); //10.46
    //或者如下
    echo number_format($num, 2, '.', ''); //10/46
```



