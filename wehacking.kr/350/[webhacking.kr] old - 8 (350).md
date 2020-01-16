<img width="287" alt="스크린샷 2020-01-15 오전 10 55 26" src="https://user-images.githubusercontent.com/54495632/72398345-03602780-3786-11ea-8a97-2412f498648e.png">

8번 

<img width="918" alt="스크린샷 2020-01-15 오전 10 55 42" src="https://user-images.githubusercontent.com/54495632/72398355-078c4500-3786-11ea-8e11-11a18fdcec58.png">


$agent=trim(getenv("HTTP_USER_AGENT"));
$ip=$_SERVER['REMOTE_ADDR'];
if(preg_match("/from/i",$agent)){
  echo("<br>Access Denied!<br><br>");
  echo(htmlspecialchars($agent));
  exit();
}

getenv("HTTP_USER_AGENT") -> 웹사이트에 접속한 컴퓨터의 웹 브라우저 정보의 값 return
trim -> 맨 앞과 맨 뒤의 여백을 제거한다.

-> 이 정보가 $agent 변수에 저장된다.

$ip -> 내 아이피 주소 저장변수

preg_match("/from/i",$agent) -> from이 필터링 된다.

$count_ck = mysqli_fetch_array(mysqli_query($db,"select count(id) from chall8")); -> 해당 테이블에서 id의 행 , 아이디 개수를 가져온다.



$result = mysqli_query($db,"select id from chall8 where agent='".addslashes($_SERVER['HTTP_USER_AGENT'])."'");

addslashes -> ' " 등 특수문자가 있으면 \ 슬래시 추가

$ck = mysqli_fetch_array($result);

if($ck){
  echo "hi <b>".htmlentities($ck[0])."</b><p>";
  if($ck[0]=="admin"){
    mysqli_query($db,"delete from chall8");
    solve(8);
  }
}

if(!$ck){
  $q=mysqli_query($db,"insert into chall8(agent,ip,id) values('{$agent}','{$ip}','guest')") or die("query error");
  echo("<br><br>done!  ({$count_ck[0]}/70)");
}

다음 두 개의 if 문을 통해 SQL INJECTION을 사용하기로 했다.
!$ck 인 상황에서 sql injection을 통해  'guest' 가 아닌 'admin' 의 값을 insert 해준다.

user agent 값 변경을 위해 burp suite를 이용했다.

<img width="803" alt="스크린샷 2020-01-15 오후 2 47 27" src="https://user-images.githubusercontent.com/54495632/72408571-95782800-37a6-11ea-9502-e287794d3795.png">

agent에 
아무 값','127.0.0.1','admin')# 하게 되면 퀴리상 나머지 뒤에 부분은 주석처리가 된다.

<img width="377" alt="스크린샷 2020-01-15 오후 2 47 34" src="https://user-images.githubusercontent.com/54495632/72408629-bb9dc800-37a6-11ea-9fd8-4ac4899ec299.png">

insert가 완료되면 다음과 같이 done 으로 처리되며

그 다음은 USER agent:test 을 다시 forward 하게되면

<img width="794" alt="스크린샷 2020-01-15 오후 2 56 42" src="https://user-images.githubusercontent.com/54495632/72408797-467ec280-37a7-11ea-884a-725843bb5775.png">


<img width="542" alt="스크린샷 2020-01-15 오후 2 48 15" src="https://user-images.githubusercontent.com/54495632/72408692-ef78ed80-37a6-11ea-9ab3-1bac2fafb4e9.png">


<img width="400" alt="스크린샷 2020-01-15 오후 2 48 22" src="https://user-images.githubusercontent.com/54495632/72408814-57c7cf00-37a7-11ea-9340-f5744333cbab.png">

해결이 가능하다.