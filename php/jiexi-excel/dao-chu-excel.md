```php
/**
 * 导出excel
 * @param $strTable    表格内容
 * @param $filename 文件名
 */
function downloadExcel($strTable,$filename)
{
   header("Content-type: application/vnd.ms-excel");
   header("Content-Type: application/force-download");
   header("Content-Disposition: attachment; filename=".$filename."_".date('Y-m-d').".xls");
   header('Expires:0');
   header('Pragma:public');
   echo '<html><meta http-equiv="Content-Type" content="text/html; charset=utf-8" />'.$strTable.'</html>';
}
public function export_user(){
   $strTable ='<table width="500" border="1">';
   $strTable .= '<tr>';
   $strTable .= '<td style="text-align:center;font-size:12px;width:120px;">会员ID</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="100">会员昵称</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">会员等级</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">手机号</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">邮箱</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">注册时间</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">最后登陆</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">余额</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">积分</td>';
   $strTable .= '<td style="text-align:center;font-size:12px;" width="*">累计消费</td>';
   $strTable .= '</tr>';
   $count = M('app_users')->count();
   $p = ceil($count/5000);
   for($i=0;$i<$p;$i++){
      $start = $i*5000;
      $end = ($i+1)*5000;
      $userList = M('app_users')->order('user_id')->limit($start.','.$end)->select();
      if(is_array($userList)){
         foreach($userList as $k=>$val){
            $strTable .= '<tr>';
            $strTable .= '<td style="text-align:center;font-size:12px;">'.$val['user_id'].'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['nickname'].' </td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['level'].'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['mobile'].'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['email'].'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.date('Y-m-d H:i',$val['reg_time']).'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.date('Y-m-d H:i',$val['last_login']).'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['user_money'].'</td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['pay_points'].' </td>';
            $strTable .= '<td style="text-align:left;font-size:12px;">'.$val['total_amount'].' </td>';
            $strTable .= '</tr>';
         }
         unset($userList);
      }
   }
   $strTable .='</table>';
   downloadExcel($strTable,'users_'.$i);
   exit();
}
```



