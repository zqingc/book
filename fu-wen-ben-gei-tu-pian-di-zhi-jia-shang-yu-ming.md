```
$content = preg_replace_callback('/<[img|IMG].*?src=[\'| \"](?![http|https])(.*?(?:[\.gif|\.jpg]))[\'|\"].*?[\/]?>/', function ($r) {
                    $str = 'http://'.$_SERVER['HTTP_HOST'].$r[1];
                    return str_replace($r[1], $str, $r[0]);
                }, $content);
```



