

利用PHP实现文字绘制到图片上的功能

```php
function syn_img_text($source, $text, $font = 'uploads/qrcode/vista.ttf') {
    $text = '@'.$text;
    $size=18;//字体大小
    $img=imagecreate(500,40);//创建一个长为500高为16的空白图片
    imagecolorallocate($img,0xff,0xff,0xff);//设置图片背景颜色，这里背景颜色为#ffffff，也就是白色
    $black=imagecolorallocate($img,0x00,0x00,0x00);//设置字体颜色，这里为#000000，也就是黑色
    imagettftext($img,$size,0,0,25,$black,$font,$text);//将ttf文字写到图片中
    //bof of 合成图片
    $child1 = imagecreatefromjpeg ( $source);
    imagecopymerge ( $child1,$img,  77, 529, 0, 0, imagesx ( $img ), imagesy ( $img ), 100 );
    //eof of 合成图片
    imagejpeg ( $child1, $source, 95 );

    imagedestroy ( $img );
    imagedestroy ( $child1 );
    return $source;
}
```



