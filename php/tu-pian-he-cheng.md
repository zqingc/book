图片合成

```php
$logo = 'qrcode/qrcode.png';  //准备好的覆盖图片
    $QR = $filename;            //原始背景图片

    if (file_exists($logo)) {
        $QR = imagecreatefromstring(file_get_contents($QR));        //目标图象连接资源。
        $logo = imagecreatefromstring(file_get_contents($logo));    //源图象连接资源。
        $QR_width = imagesx($QR);           //原始背景图片宽度
        $QR_height = imagesy($QR);          //原始背景图片高度
        $logo_width = imagesx($logo);       //覆盖图片图片宽度
        $logo_height = imagesy($logo);      //覆盖图片图片高度
        $logo_qr_width = $QR_width / 5;     //组合之后覆盖图片的宽度(占原始背景图片的1/5)
        $scale = $logo_width/$logo_qr_width;    //覆盖图片的宽度缩放比(本身宽度/组合后的宽度)
        $logo_qr_height = $logo_height/$scale;  //组合之后覆盖图片的高度
        $from_width = ($QR_width - $logo_qr_width) / 2;   //组合之后覆盖图片左上角所在坐标点

        //重新组合图片并调整大小
        /*
         *  imagecopyresampled() 将一幅图像(源图象)中的一块正方形区域拷贝到另一个图像中
         */
        imagecopyresampled($QR, $logo, $from_width, $from_width, 0, 0, $logo_qr_width,$logo_qr_height, $logo_width, $logo_height);
    }
    imagejpeg($QR,$filename);

    return '/'.$filename;
```



