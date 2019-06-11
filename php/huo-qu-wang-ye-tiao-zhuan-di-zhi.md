```php
<?php

    $url = "https://dibaqu.com/show/download/17222?pwd=";
    $headers = get_headers($url, TRUE);
    print_r($headers);

    //输出跳转到的网址
    echo $headers['location'];

?>
```



