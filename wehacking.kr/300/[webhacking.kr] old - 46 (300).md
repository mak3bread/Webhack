<img width="285" alt="스크린샷 2020-01-13 오후 2 08 51" src="https://user-images.githubusercontent.com/54495632/72234054-5fa03b80-360e-11ea-9e6e-7d0b21519258.png">

46번 300

<img width="307" alt="스크린샷 2020-01-13 오후 2 09 00" src="https://user-images.githubusercontent.com/54495632/72234059-6af36700-360e-11ea-97f7-7b5c66a0d735.png">

친절하게 SQL Injection 임을 알려준다.

<img width="806" alt="스크린샷 2020-01-13 오후 2 09 09" src="https://user-images.githubusercontent.com/54495632/72234065-76469280-360e-11ea-9e80-44d0bf8eea9e.png">

소스코드를 보면,

$_GET['lv'] = addslashes($_GET['lv']);
$_GET['lv'] = str_replace(" ","",$_GET['lv']);
$_GET['lv'] = str_replace("/","",$_GET['lv']);
$_GET['lv'] = str_replace("*","",$_GET['lv']);
$_GET['lv'] = str_replace("%","",$_GET['lv']);

addslashes 함수는 파라미터로 넘어온 문자열 안에 ' , " , \ , NULL 바이트가 포함되어 있다면 해당 문자 앞에 역슬래시 \를 추가해 주는 함수이다.

또한 , 위 코드에서 str_replace에 의해 공백, \ , * , % 등이 필터링 된다.

if(preg_match("/select|0x|limit|cash/i",$_GET['lv'])) exit();
prog_match에 의해 select, 0x, limit , cash 등이 필터링 된다.

필터링 조건이 많지만 간단한 문제이다.
id='admin' 을 맞춰주면 된다.

lv=0||id=char(97,100,109,105,110) 로 해결 가능하다.

<img width="492" alt="스크린샷 2020-01-13 오후 2 50 10" src="https://user-images.githubusercontent.com/54495632/72235205-279bf700-3614-11ea-930c-ba4a51265580.png">