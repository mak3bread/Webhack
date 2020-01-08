<img width="281" alt="스크린샷 2020-01-08 오후 11 12 08" src="https://user-images.githubusercontent.com/54495632/71985628-48f49000-326e-11ea-8ae9-6ee26e00a1ea.png">

7번

<img width="149" alt="스크린샷 2020-01-08 오후 11 12 16" src="https://user-images.githubusercontent.com/54495632/71985631-4b56ea00-326e-11ea-920e-5c634cad24e5.png">

<img width="449" alt="스크린샷 2020-01-08 오후 11 12 22" src="https://user-images.githubusercontent.com/54495632/71985643-50b43480-326e-11ea-915e-9ff9e76f4a6a.png">

auth 를 누르게 되면 접근이 거부가 된다.

view - source 를 보면,

<img width="896" alt="스크린샷 2020-01-08 오후 11 12 54" src="https://user-images.githubusercontent.com/54495632/71985689-61fd4100-326e-11ea-9373-84c104ee43c9.png">

else if 문을 보면 쿼리 결과가 2 가 나와야 solve 가 되는 문제이다.

$data=mysqli_fetch_array($result); $result 를 2로 만들어 $data 에 저장하면 된다.

if($rand==1){
  $result=mysqli_query($db,"select lv from chall7 where lv=($go)") or die("nice try!");
}
if($rand==2){
  $result=mysqli_query($db,"select lv from chall7 where lv=(($go))") or die("nice try!");
}
if($rand==3){
  $result=mysqli_query($db,"select lv from chall7 where lv=((($go)))") or die("nice try!");
}
if($rand==4){
  $result=mysqli_query($db,"select lv from chall7 where lv=(((($go))))") or die("nice try!");
}
if($rand==5){
  $result=mysqli_query($db,"select lv from chall7 where lv=((((($go)))))") or die("nice try!");
}

$result 가 정의 되는 괄호 조건이 5개 인데 () 로 괄호 하나만 쓰는 형태를 이용 하기로 했다.

20%확률로 성립할 것 같다.

preg_match("/2|-|\+|from|_|=|\\s|\*|\//i",$go)) exit("Access Denied!");

preg_match 의 함수에 의해서 2, - , + , from , _ , = , s . *, 1개 이상 \ , 모든 공백, / 등 필터링 되는

조건이 있다. val=2 로는 바로 접근할 수 없을 것 같다.

<img width="533" alt="스크린샷 2020-01-09 오전 12 12 42" src="https://user-images.githubusercontent.com/54495632/71989308-c6230380-3274-11ea-8b50-5790a75b04e1.png">

혹시나 했지만 역시나 되지 않는다. 2를 간접적으로 넣으면서 필터링 조건을 피하는 injection 방법을

생각했다. sqrt(4) -> 2 가 가능하고 괄호와 # 로 주석 처리가 가능하다.

따라서 필터링을 피하여 SELECT lv FROM chall7 WHERE lv = (0)UNION(SELECT(SQRT(4))#)

와 같이 전체 쿼리를 넣었고 val=0 뒤에 넣어야될 url 부분은 )UNION(SELECT(SQRT(4))#) 이다.

<img width="656" alt="스크린샷 2020-01-09 오전 12 07 42" src="https://user-images.githubusercontent.com/54495632/71989594-4c3f4a00-3275-11ea-9f7f-319b42a6f2ea.png">

확률이 1/5 라서 실패한 경우 .. 그냥 nice try라고만 출력해준다.

해당 쿼리로 여러 번 시도하다 보면

<img width="446" alt="스크린샷 2020-01-09 오전 12 08 32" src="https://user-images.githubusercontent.com/54495632/71989640-5cefc000-3275-11ea-8e2a-4b3235745300.png">

문제 해결이 가능하다.