
/* @stmt 需下载的数据，类型 [[ ]]
*  @head 下载数据列名 , 类型 [] 
*  @filename 文件名 
*/

function xiazai($stmt,$head,$filename) { 
set_time_limit(0); 
header('Content-Type: application/vnd.ms-excel'); 
header('Content-Disposition: attachment;filename='.$filename); 
$fp = fopen('php://output', 'a'); 

foreach ($head as $i => $v) {
  $head[$i] = $v; 
} 

fputcsv($fp, $head); 
$cnt = 0; 
$limit = 100000; 

foreach ($stmt as $va){
  $cnt ++; 
  if ($limit == $cnt) { 
    ob_flush();
    flush(); 
    $cnt = 0; 
  } 
  
  foreach ($va as $i => $v) { 
  $row[$i] = $v?$v:'-'; 
  } 
fputcsv($fp, $row); 
}
