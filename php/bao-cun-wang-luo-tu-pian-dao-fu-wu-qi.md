保存网络图片到服务器

```php
//保存微信头像到本地
function saveImage($url) {
    $header = array(
        'User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:45.0) Gecko/20100101 Firefox/45.0',
        'Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3',
        'Accept-Encoding: gzip, deflate',);
    $url='http://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTKkGpNuUhaBniatRsiaG7ksqmhUWzkk40kTRS6icQS7kJcsfxcibQo7vDFcKibr7NHb9YIXiaXsEtLcdL6A/0';
    $curl = curl_init();curl_setopt($curl, CURLOPT_URL, $url);curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($curl, CURLOPT_FOLLOWLOCATION, true);curl_setopt($curl, CURLOPT_ENCODING, 'gzip');
    curl_setopt($curl, CURLOPT_HTTPHEADER, $header);$data = curl_exec($curl);$code = curl_getinfo($curl, CURLINFO_HTTP_CODE);curl_close($curl);
    if ($code == 200) {//把URL格式的图片转成base64_encode格式的！
        $imgBase64Code = "data:image/jpeg;base64," . base64_encode($data);
    }
    $img_content=$imgBase64Code;//图片内容
    //echo $img_content;exit;
    if (preg_match('/^(data:\s*image\/(\w+);base64,)/', $img_content, $result))
    {
        $type = $result[2];//得到图片类型png?jpg?gif?
        $new_file = 'qrcode/'.date('Ymd',time()).'/'.time().'1.'.$type;
        if (file_put_contents($new_file, base64_decode(str_replace($result[1], '', $img_content)))){
            return $new_file;die;
        }
    }
    return 0;die;
}
//下载网络图片到本地
function saveImage1($path) {
    if(!preg_match('/\/([^\/]+\.[a-z]{3,4})$/i',$path,$matches)){
        die('Use image please');
    }
    $image_name = strToLower($matches[1]);
    $ch = curl_init ($path);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_BINARYTRANSFER,1);
    $img = curl_exec ($ch);
    curl_close ($ch);
    $fp = fopen($image_name,'w');
    fwrite($fp, $img);
    fclose($fp);
    return $image_name;
}
```



