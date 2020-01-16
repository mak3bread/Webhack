<img width="282" alt="스크린샷 2020-01-15 오후 3 00 00" src="https://user-images.githubusercontent.com/54495632/72409178-5cd94e00-37a8-11ea-93ea-8bfe112e2174.png">

35번 .

<img width="459" alt="스크린샷 2020-01-15 오후 3 00 08" src="https://user-images.githubusercontent.com/54495632/72409198-68c51000-37a8-11ea-84e7-6d059badd200.png">

form 으로 phone 정보를 받는다. 다른건 모르겠다.
view - source를 보자.

<img width="1024" alt="스크린샷 2020-01-15 오후 3 00 30" src="https://user-images.githubusercontent.com/54495632/72409283-99a54500-37a8-11ea-8b2c-3c3fa10542ba.png">


if(preg_match("/\*|\/|=|select|-|#|;/i",$_GET['phone'])) exit("no hack");
Get 형태로 phone 정보를 받는다.
preg_match로 * / select = - # 등이 필터링 된다.

if(strlen($_GET['id']) > 5) exit("no hack");
get으로 id를 받는데 id 문자열의 길이가 5가 넘으면 안된다.

if(preg_match("/admin/i",$_GET['id'])) exit("you are not admin");
id = admin으로 되는 것을 필터링한다. 

mysqli_query($db,"insert into chall35(id,ip,phone) values('{$_GET['id']}','{$_SERVER['REMOTE_ADDR']}',{$_GET['phone']})") or die("query error");

쿼리에 들어가는 순서는 id - 아이피 - phone 순서이다.

insert는 다중 데이터를 입력할 수 있다.
insert into chall35(id,ip,phone) values(id,ip,phone),(1,2,3) 과 같이 가능하다.


1),('admin','1.11.213.246','2' 와 같이 입력하여 SQL INJECTION을 진행하였다.

<img width="387" alt="스크린샷 2020-01-15 오후 3 13 38" src="https://user-images.githubusercontent.com/54495632/72410247-4ed8fc80-37ab-11ea-819f-b8b424fdb0a3.png">

<img width="596" alt="스크린샷 2020-01-15 오후 3 13 53" src="https://user-images.githubusercontent.com/54495632/72410252-50a2c000-37ab-11ea-812a-c542837adb78.png">