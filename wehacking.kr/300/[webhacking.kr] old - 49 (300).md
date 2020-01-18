<img width="281" alt="스크린샷 2020-01-13 오후 2 52 33" src="https://user-images.githubusercontent.com/54495632/72235267-8bbebb00-3614-11ea-98f3-f5b0a719d830.png">

49번 300!

<img width="281" alt="스크린샷 2020-01-13 오후 2 52 33" src="https://user-images.githubusercontent.com/54495632/72235273-911c0580-3614-11ea-9d95-c826453a6842.png">

방금 풀었던 46번과 같아서 잘못들어온줄 알았다...
view-source로 소스코드를 보자.

<img width="804" alt="스크린샷 2020-01-13 오후 2 52 50" src="https://user-images.githubusercontent.com/54495632/72235291-aabd4d00-3614-11ea-973e-b02ef320c133.png">

if($_GET['lv']){
아까와 같이 lv를 GET으로 받는다.

if(preg_match("/select|or|and|\(|\)|limit|,|\/|order|cash| |\t|\'|\"/i",$_GET['lv'])) exit("no hack");

select, or , and, \, 괄호, limit, / , order, cash, 탭 , 작은 따옴표, 큰 따옴표 등 필터링 되는 조건이 많다..

$result = mysqli_fetch_array(mysqli_query($db,"select id from chall49 where lv={$_GET['lv']}"));
쿼리도 아까와 비슷하며 where절에 lv가 오고 
if($result[0]=="admin") solve(49);
$result에 admin이 오면 해결이 된다.

hex가 막혀 있지 않아 admin으로 0x61646d696e 를 주고
or이 필터링되서 대신 || 로 or을 대체했다. 간단한 문제이다.

lv=0||id=0x61646d696e 로 해결

<img width="491" alt="스크린샷 2020-01-13 오후 2 59 33" src="https://user-images.githubusercontent.com/54495632/72235427-7dbd6a00-3615-11ea-9384-a83404eeb323.png">