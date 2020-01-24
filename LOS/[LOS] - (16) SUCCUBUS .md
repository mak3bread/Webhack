<img width="232" alt="스크린샷 2020-01-24 오후 5 39 10" src="https://user-images.githubusercontent.com/54495632/73055986-50a06f80-3ed1-11ea-9c70-f9124b65acdb.png">

16번 서큐버스

<img width="713" alt="스크린샷 2020-01-24 오후 5 39 17" src="https://user-images.githubusercontent.com/54495632/73056210-cf95a800-3ed1-11ea-9a66-da15f679cc16.png">

생각보다 문제가 간단하다.

if(preg_match('/\'/',$_GET[id])) exit("HeHe");
if(preg_match('/\'/',$_GET[pw])) exit("HeHe");

preg_match로 id와 pw에서 ' 작은 따옴표가 필터링 된다.

따른 조건이 없어 \ 로 우회하였다.

$query = "select id from prob_succubus where id='{$_GET[id]}' and pw='{$_GET[pw]}'"; 

\ escape 을 이용하여
기본 쿼리문에서 URL로 ?id=\ 를 입력하게 되면(where 앞 절 생략)
 id='\' and pw='' 와 같이 쿼리가 구성된다. 이 때 \' 는 작은 따옴표의 역할을 못하고
문자열 ' 로 쓰이게 된다.

즉 id = '\' and pw= '' 에서 id에 \' and pw = 라는 값이 입력되고 마지막 '가 남는다.

id='false' ' -> 인 상황

id = 다음 좌변이 false 이므로 || or 연산자와 함께 우변의 조건을 TRUE 맞추면
전체 WHERE절을 TRUE로 만들 수 있다.

<img width="747" alt="스크린샷 2020-01-24 오후 10 21 41" src="https://user-images.githubusercontent.com/54495632/73073483-ca991e80-3efa-11ea-969d-eb1751341251.png">