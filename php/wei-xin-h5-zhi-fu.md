```php
public function h5pay(){
    $order_id = input('id');
    $order = Db::name('order')->where(array('id'=>$order_id))->find();
    if(!$order){
        $this->error('订单不存在');die;
    }
    $config = get_gameconfig('wechatpay');

    /*$appid = 'wxde7e5ad266a1ec56';
    $mch_id = '1500713701';//商户号
    $key = 'hw56jFYU24h23j32hrVtyH673fuihewf';//商户key*/

    $notify_url = "http://".$_SERVER['SERVER_NAME'].'/wechatpay.php';//回调地址
    $wechatAppPay = new wechatH5Pay($config['appid'], $config['mch_id'], $notify_url, $config['key']);
    if(empty($order['shop_name'])){
        $params['body'] = '道具';
    }else{
        $params['body'] = $order['shop_name'];
    }              //商品描述
    $params['out_trade_no'] = $order['ordernumber'];    //自定义的订单号
    $params['total_fee'] =  $order['money'];        //订单金额 只能为整数 单位为分
    $params['trade_type'] = 'MWEB';                   //交易类型 JSAPI | NATIVE | APP | WAP
    $params['scene_info'] = '{"h5_info": {"type":"Wap","wap_url": "http://'.DOMAIN_NAMES.'","wap_name": '.$order['shop_name'].'}}';

    $result = $wechatAppPay->unifiedOrder( $params );

    $url = $result['mweb_url'].'&redirect_url=http%3A%2F%2F'.DOMAIN_NAMES.'/index.php/index/pay/index/id/'.$order_id;//redirect_url 是支付完成后返回的页面
    $this->assign('url',$url);
    return $this->fetch();
}
```



