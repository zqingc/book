```php
public function __construct(Request $request = null)
{
    parent::__construct($request);
    $this->appid = 'wxde7e5ad266a1ec56';//appid
    $this->secret = '24fab79d5915bc12b079ed4a52a2956e'; //secrect
}
//第一步获得code
public function login()
{
    if(Session::has('member_ids'))//判断用户是否登录过如果登陆过
    {
        $member_id = model('member')->field('id')->where(['id'=>Session::get('member_id')])->find()['id'];
        if($member_id){//判断用户在数据库中是否有记录如果没有记录就清空登录状态重新发起userinfo方式用户授权
             $this->redirect('http://'.$_SERVER['HTTP_HOST'].'/index.php/member/index');die;
        }
        Session::set('member_ids',null);
    }
    $callback = 'http://' . $_SERVER['HTTP_HOST'] . '/index.php/member/login/index';
    $url = 'https://open.weixin.qq.com/connect/oauth2/authorize?appid=' . $this->appid . '&redirect_uri=' . $callback . '&response_type=code&scope=snsapi_userinfo&state=2&connect_redirect=1#wechat_redirect';
    header("Location:" . $url);
}
//第二步 判断code，获得用户信息
public function index()
{
    $code = $_GET["code"];
    if (isset($_GET['code'])){
        $userinfo = $this->get_user_info($code);
        $wechat_id = model('member_wechat')->where(['unionid'=>$userinfo['unionid']])->value('id')
        if($wechat_id){
            model('member_wechat')->where(['id'=>$wechat_id])->update($userinfo);//将数据写入到数据库
        }else{
            model('member_wechat')->insert($userinfo);//将数据写入到数据库
        }
        $member_id = model('member')->field('id')->where(['unionid'=>$userinfo['unionid']])->find()['id'];
        if(!$member_id){
            $data = array(
                'unionID'      =>    $userinfo['unionid'],
                'nickname'    =>    $userinfo['nickname'],//呢称
                'photo'       =>    $userinfo['headimgurl'],//头像
                'sex'         =>    $userinfo['sex'],//性别
                'reg_time'    =>    time(),
                'login_time'  =>    time(),
                'login_ip'    =>    get_client_ip(),
                'status'      =>    1,
            );
            $member_id = model('member')->insertGetId($data);
        }else{
            $data = array(
                'nickname'    =>    $userinfo['nickname'],//呢称
                'photo'       =>    $userinfo['headimgurl'],//头像
                'login_time'  =>    time(),
                'login_ip'    =>    get_client_ip(),
            );
            model('member')->where(['id'=>$member_id])->insertGetId($data);
        }
        Session::set('member_ids',$member_id);
        $this->redirect('http://'.$_SERVER['HTTP_HOST'].'/index.php/member/index');die;
    }else{
        echo "<h1>授权错误，请重试</h1>";
    }
}
public function get_user_info($code)
{
    $access_token_url = "https://api.weixin.qq.com/sns/oauth2/access_token?appid=". $this->appid ."&secret=".$this->secret. "&code=".$code. "&grant_type=authorization_code";
    $access_token_json = $this->https_request($access_token_url);//自定义函数
    $access_token_array = json_decode($access_token_json,true);
    $access_token = $access_token_array['access_token'];
    $openid = $access_token_array['openid'];
    $userinfo_url = "https://api.weixin.qq.com/sns/userinfo?access_token=$access_token&openid=$openid";
    $userinfo_json = $this->https_request($userinfo_url);
    $userinfo_array = json_decode($userinfo_json,true);
    return $userinfo_array;
}
public function https_request($url)//访问url返回结果
{
    $curl = curl_init();
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);
    curl_setopt($curl,  CURLOPT_SSL_VERIFYHOST, FALSE);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    $data = curl_exec($curl);
    if (curl_errno($curl)){
        return 'ERROR'.curl_error($curl);
    }
    curl_close($curl);
    return $data;
}
```



