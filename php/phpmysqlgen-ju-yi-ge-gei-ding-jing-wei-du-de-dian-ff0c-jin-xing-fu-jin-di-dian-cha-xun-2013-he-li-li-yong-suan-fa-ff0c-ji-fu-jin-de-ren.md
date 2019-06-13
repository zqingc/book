PHP,Mysql-根据一个给定经纬度的点，进行附近地点查询–合理利用算法，即附近的人

```php
define(EARTH_RADIUS, 6371);//地球半径，平均半径为6371km
 /**
 *计算某个经纬度的周围某段距离的正方形的四个点
 *
 *@param lng float 经度
 *@param lat float 纬度
 *@param distance float 该点所在圆的半径，该圆与此正方形内切，默认值为0.5千米
 *@return array 正方形的四个点的经纬度坐标
 */
 function returnSquarePoint($lng, $lat,$distance = 0.5){
 
    $dlng =  2 * asin(sin($distance / (2 * EARTH_RADIUS)) / cos(deg2rad($lat)));
    $dlng = rad2deg($dlng);
     
    $dlat = $distance/EARTH_RADIUS;
    $dlat = rad2deg($dlat);
     
    return array(
                'left-top'=>array('lat'=>$lat + $dlat,'lng'=>$lng-$dlng),
                'right-top'=>array('lat'=>$lat + $dlat, 'lng'=>$lng + $dlng),
                'left-bottom'=>array('lat'=>$lat - $dlat, 'lng'=>$lng - $dlng),
                'right-bottom'=>array('lat'=>$lat - $dlat, 'lng'=>$lng + $dlng)
                );
 }
//使用此函数计算得到结果后，带入sql查询。
$squares = returnSquarePoint($lng, $lat);
$info_sql = "select id,locateinfo,lat,lng from `lbs_info` where lat<>0 and lat>{$squares['right-bottom']['lat']} and lat<{$squares['left-top']['lat']} and lng>{$squares['left-top']['lng']} and
 lng<{$squares['right-bottom']['lng']} "; 
```



