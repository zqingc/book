时间戳

1.PHP时间戳函数将日期转化为unix时间戳

```php
echo "世界末日时间戳为：".strtotime("2012-12-21")
```

2.将时间戳转化为系统时间

```php
date('Y-m-d H:i:s',"1228348800");
```

（1）获取当天零点时间戳

```php
$timetoday = strtotime(date("Y-m-d",time()));
```

（2）获取明天零点时间戳

```php
$tomorrow = $timetoday + 3600*24;
```

3.PHP时间戳函数获取英文文本日期时间 示例如下：

便于比较，使用date将当时间戳与指定时间戳转换成系统时间

\(1\)打印明天此时的时间戳strtotime\(”+1 day”\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()); 
//明天此时时间 
echo date("Y-m-d H:i:s",strtotime("+1 day"));

```

\(2\)打印昨天此时的时间戳strtotime\(”-1 day”\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()) ; 
//指定时间 
echo date("Y-m-d H:i:s",strtotime("-1 day"));

```

\(3\)打印下个星期此时的时间戳strtotime\("+1 week"\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()); 
//下星期时间 
echo date("Y-m-d H:i:s",strtotime("+1 week"));

```

\(4\)打印上个星期此时的时间戳strtotime\("-1 week"\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()); 
//上个星期此时时间 
echo date("Y-m-d H:i:s",strtotime("-1 week"));

```

\(5\)打印指定下星期几的时间戳strtotime\("next Thursday"\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()); 
//下星期几时间 
echo date("Y-m-d H:i:s",strtotime("next Thursday"));
```

\(6\)打印指定上星期几的时间戳strtotime\(”last Thursday”\)

```php
//当前时间 
echo date("Y-m-d H:i:s",time()); 
//指定时间 
echo date("Y-m-d H:i:s",strtotime("last Thursday"));

```



```php
/**
 * 友好时间显示
 * @param $time
 * @return bool|string
 */
function friend_date($time)
{
    if (!$time)
        return false;
    $fdate = '';
    $d = time() - intval($time);
    $ld = $time - mktime(0, 0, 0, 0, 0, date('Y')); //得出年
    $md = $time - mktime(0, 0, 0, date('m'), 0, date('Y')); //得出月
    $byd = $time - mktime(0, 0, 0, date('m'), date('d') - 2, date('Y')); //前天
    $yd = $time - mktime(0, 0, 0, date('m'), date('d') - 1, date('Y')); //昨天
    $dd = $time - mktime(0, 0, 0, date('m'), date('d'), date('Y')); //今天
    $td = $time - mktime(0, 0, 0, date('m'), date('d') + 1, date('Y')); //明天
    $atd = $time - mktime(0, 0, 0, date('m'), date('d') + 2, date('Y')); //后天
    if ($d == 0) {
        $fdate = '刚刚';
    } else {
        switch ($d) {
            case $d < $atd:
                $fdate = date('Y年m月d日', $time);
                break;
            case $d < $td:
                $fdate = '后天' . date('H:i', $time);
                break;
            case $d < 0:
                $fdate = '明天' . date('H:i', $time);
                break;
            case $d < 60:
                $fdate = $d . '秒前';
                break;
            case $d < 3600:
                $fdate = floor($d / 60) . '分钟前';
                break;
            case $d < $dd:
                $fdate = floor($d / 3600) . '小时前';
                break;
            case $d < $yd:
                $fdate = '昨天' . date('H:i', $time);
                break;
            case $d < $byd:
                $fdate = '前天' . date('H:i', $time);
                break;
            case $d < $md:
                $fdate = date('m月d日 H:i', $time);
                break;
            case $d < $ld:
                $fdate = date('m月d日', $time);
                break;
            default:
                $fdate = date('Y年m月d日', $time);
                break;
        }
    }
    return $fdate;
}
```



