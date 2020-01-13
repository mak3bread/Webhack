<img width="287" alt="스크린샷 2020-01-13 오후 1 36 40" src="https://user-images.githubusercontent.com/54495632/72233544-55c90900-360b-11ea-94be-015055b3f569.png">

11번 300

<img width="149" alt="스크린샷 2020-01-13 오후 1 36 52" src="https://user-images.githubusercontent.com/54495632/72233548-5c578080-360b-11ea-8596-ebace33d9845.png">

첫 화면 , view-source로 소스코드를 보자.

<img width="526" alt="스크린샷 2020-01-13 오후 1 37 18" src="https://user-images.githubusercontent.com/54495632/72233558-66797f00-360b-11ea-8f16-0dde845c3cad.png">

생각보다 php 소스가 짧다.
정규 표현식에 관련된 내용인데 
다음의 블로그?를 참조했다.
https://hamait.tistory.com/342

$pat에 정규 표현식이 저장되고 해당 값이 맞게 되면 solve가 된다.

$pat="/[1-3][a-f]{5}_.*$_SERVER[REMOTE_ADDR].*\tp\ta\ts\ts/";

다음 정규 표현식을 해석하면,
[1-3] -> 1 부터 3 사이의 값을 입력한다.
[a-f]{5}_ -> a 부터 f 사이의 문자 중 5번 입력한 후 마지막에 _ 값을 입력한다.
.* - .이 0회 이상 -. 표현
_SERVER[REMOTE_ADDR]-> 이건 사용자 아이피
\t - tab -> URL %09


if(preg_match($pat,$_GET['val'])){
    solve(11);
  }
여기서 , $pat이 URL val로 입력되므로 정리하면

?val=1aaaaa_.아이피.%09p%09a%09s%09s

<img width="510" alt="스크린샷 2020-01-13 오후 2 01 58" src="https://user-images.githubusercontent.com/54495632/72233905-611d3400-360d-11ea-8c58-9266594d3a22.png">

<img width="510" alt="스크린샷 2020-01-13 오후 2 01 58" src="https://user-images.githubusercontent.com/54495632/72233908-64b0bb00-360d-11ea-9791-6111848838d9.png">

정규 표현식의 개념을 이용하는 비교적 간단한 문제였다.



# 정규표현식 정리

[x - z]  x~z 사이의 문자 중 하나를 찾는다.
x{n}    x를 n번 반복한 문자를 찾는다.
.x        임의의 한 문자를 표현한다.
x*       x가 0번이상 반복한다.
\t        tab 문자를 찾는다.