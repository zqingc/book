使用phpqrcode生成二维码

前期准备:

1.phpqrcode类文件下载，下载地址：

[https://sourceforge.net/projects/phpqrcode/](https://sourceforge.net/projects/phpqrcode/)

2.PHP环境必须开启支持GD2扩展库支持（一般情况下都是开启状态）

  


方法解读：

下载下来的类文件是一个压缩包，里边包含很多文件和演示程序，我们只需要里边的phpqrcode.php这一个文件就可以生成二维码了。它是一个多个类的集合文件，我们需要用到里边的QRcode类（第2963行）的png\(\)方法（第3090行）：

```php
public static function png($text, $outfile = false, $level = QR_ECLEVEL_L, $size = 3, $margin = 4, $saveandprint=false)
{
$enc = QRencode::factory($level, $size, $margin);
return $enc->encodePNG($text, $outfile, $saveandprint=false);
}
```

第1个参数$text：二维码包含的内容，可以是链接、文字、json字符串等等；

第2个参数$outfile：默认为false，不生成文件，只将二维码图片返回输出；否则需要给出存放生成二维码图片的文件名及路径；

第3个参数$level：默认为L，这个参数可传递的值分别是L\(QR\_ECLEVEL\_L，7%\)、M\(QR\_ECLEVEL\_M，15%\)、Q\(QR\_ECLEVEL\_Q，25%\)、H\(QR\_ECLEVEL\_H，30%\)，这个参数控制二维码容错率，不同的参数表示二维码可被覆盖的区域百分比，也就是被覆盖的区域还能识别；

第4个参数$size：控制生成图片的大小，默认为4；

第5个参数$margin：控制生成二维码的空白区域大小；

第6个参数$saveandprint：保存二维码图片并显示出来，$outfile必须传递图片路径；

  


使用示例：

1. 生成二维码\(生成图片文件\)

```php
function scerweima($url=''){
require_once 'phpqrcode.php';
$value = $url; //二维码内容
$errorCorrectionLevel = 'L'; //容错级别
$matrixPointSize = 5; //生成图片大小 
//生成二维码图片
$filename = 'qrcode/'.microtime().'.png';
QRcode::png($value,$filename , $errorCorrectionLevel, $matrixPointSize, 2);
$QR = $filename; //已经生成的原始二维码图片文件 
$QR = imagecreatefromstring(file_get_contents($QR));
//输出图片 
imagepng($QR, 'qrcode.png');
imagedestroy($QR);
return '<img src="qrcode.png" alt="使用微信扫描支付">';
}
//调用查看结果
echo scerweima('https://www.baidu.com');
```

2.在生成的二维码中加上logo\(生成图片文件\)

```php
function scerweima1($url=''){
require_once 'phpqrcode.php';
$value = $url; //二维码内容 
$errorCorrectionLevel = 'H'; //容错级别 
$matrixPointSize = 6; //生成图片大小 
//生成二维码图片
$filename = 'qrcode/'.microtime().'.png';
QRcode::png($value,$filename , $errorCorrectionLevel, $matrixPointSize, 2);
$logo = 'qrcode/logo.jpg'; //准备好的logo图片 
$QR = $filename; //已经生成的原始二维码图 
if (file_exists($logo)) {
$QR = imagecreatefromstring(file_get_contents($QR)); //目标图象连接资源。
$logo = imagecreatefromstring(file_get_contents($logo)); //源图象连接资源。
$QR_width = imagesx($QR); //二维码图片宽度 
$QR_height = imagesy($QR); //二维码图片高度 
$logo_width = imagesx($logo); //logo图片宽度 
$logo_height = imagesy($logo); //logo图片高度 
$logo_qr_width = $QR_width / 4; //组合之后logo的宽度(占二维码的1/5)
$scale = $logo_width/$logo_qr_width; //logo的宽度缩放比(本身宽度/组合后的宽度)
$logo_qr_height = $logo_height/$scale; //组合之后logo的高度
$from_width = ($QR_width - $logo_qr_width) / 2; //组合之后logo左上角所在坐标点
//重新组合图片并调整大小
/*
* imagecopyresampled() 将一幅图像(源图象)中的一块正方形区域拷贝到另一个图像中
*/
imagecopyresampled($QR, $logo, $from_width, $from_width, 0, 0, $logo_qr_width,$logo_qr_height, $logo_width, $logo_height);
}
//输出图片 
imagepng($QR, 'qrcode.png');
imagedestroy($QR);
imagedestroy($logo);
return '<img src="qrcode.png" alt="使用微信扫描支付">';
}
//调用查看结果
echo scerweima1('https://www.baidu.com');
```

3. 生成二维码\(不生成图片文件\)

```php
function scerweima2($url=''){
require_once 'phpqrcode.php';
$value = $url; //二维码内容
$errorCorrectionLevel = 'L'; //容错级别
$matrixPointSize = 5; //生成图片大小 
//生成二维码图片
$QR = QRcode::png($value,false,$errorCorrectionLevel, $matrixPointSize, 2);
}
//调用查看结果
scerweima2('https://www.baidu.com');
```

\*前两种方法，每调用一次都会在本地生成一张二维码图片，第三种方法，不生成文件，会直接输出二维码到浏览器中。

