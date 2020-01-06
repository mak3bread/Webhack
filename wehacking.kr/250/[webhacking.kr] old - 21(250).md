
<img width="284" alt="스크린샷 2020-01-05 오후 6 52 49" src="https://user-images.githubusercontent.com/54495632/71819140-5f63e580-30ce-11ea-90b8-b77b95350a18.png">

21 번

<img width="472" alt="스크린샷 2020-01-05 오후 6 52 59" src="https://user-images.githubusercontent.com/54495632/71819145-668af380-30ce-11ea-822d-3681278d6b91.png">


문제에 들어가면, BLIND SQL INJECTION 이라고 친절하게 알려준다.

\#Blind Sql Injection 이란?

SQL 질의문 입력으로 나오는 참, 거짓 결과를 이용하여 해당 결과 값을 보고 DB 안의

데이터나 구조를 파악하는 기법을 의미한다.

<img width="515" alt="스크린샷 2020-01-05 오후 7 03 53" src="https://user-images.githubusercontent.com/54495632/71819165-7276b580-30ce-11ea-92a7-9564eb9143c4.png">


id 와 pw 두 개의 폼으로 받는 구조이다.

<img width="416" alt="스크린샷 2020-01-05 오후 10 48 16" src="https://user-images.githubusercontent.com/54495632/71819190-8b7f6680-30ce-11ea-9657-2d7fa3e27663.png">


Blind SQL injection 기반으로 True / False 를 받아서 데이터 베이스 안의 정보를

받아보려고 했으나 True false 정보는 표시를 해주지 않는 구조 인 것 같아

Time based SQL injection 을 사용했다.

time based SQL injection 을 이용하게 되면 해당 조건이 참일 시 웹페이지가 sleep

함수에 의해 리로딩 되며 false 인 경우 바로 웹페이지가 새로고침 될 것이다.

기본적인 쿼리는 User 테이블이라고 가정 했을 때

select * from user where id ='admin' and pw=' or length(pw)<값 AND Sleep(2))

처음에는 id = admin를 주고

pw 에 ' or (length(pw)<100 AND Sleep(2))# 를 주어

pw 의 길이를 구하려고 했다. 100 - 50 - 25 - 37 과 같은 방법으로 구하여

' or (length(pw)>37 AND Sleep(2))# 일 때는 sleep 함수가 동작하지 않았다.

' or (length(pw)=36 AND Sleep(2))# 일 때 sleep 함수가 동작하여 페이지가 로딩된다.

<img width="422" alt="스크린샷 2020-01-06 오후 6 46 03" src="https://user-images.githubusercontent.com/54495632/71819227-a225bd80-30ce-11ea-91f0-fe4411a939e3.png">


Time based SQL injection 만 가능하다고 생각했는데

맞는 값이 들어올 시 'wrong password' 로 문구가 변하는 것 같다.

True -> wrong password

false -> login fail

로 출력이 되는 것 같다.

그래서 sleep을 사용하지 않고

' or (ascii(substr(pw,1,1))=116 #

이런 식으로 쿼리를 넣었다.

<img width="417" alt="스크린샷 2020-01-06 오후 6 51 16" src="https://user-images.githubusercontent.com/54495632/71819244-ac47bc00-30ce-11ea-9b9f-3d18aae3dda0.png">


실행 전.

<img width="503" alt="스크린샷 2020-01-06 오후 6 51 24" src="https://user-images.githubusercontent.com/54495632/71819259-b36eca00-30ce-11ea-9869-95f91c2abf0b.png">


sleep 을 쓰지 않아도 되는 것 같다.

pw 자리수와 id 를 얻어 쿼리를 변경하여

pw를 얻기로 했다.

substr 과 ascii 를 사용했는데

substr(pw , 1 , 1) 과 같이 주면 pw의 첫 째 자리에서 한 자리의 문자를 가져온다.

ascii(해당문자) 는 해당 문자를 아스키 번호로 변경 시켜 준다.

이를 boolean, true false 로 변경하기 위해 쿼리 문을

' or ascii(substr(pw,1,1))<120 # 과 같은 형식으로 만들었다.

해당 쿼리문의 의미는 pw의 첫 째 자리 문자의 아스키코드값이 120 보다 작으면

웹페이지의 Result : 에 wrong password 를 띄우게 될 것이다.

이를 36번 반복하게 되면 전체 문자를 얻을 수 있지만 너무

복잡하여 파이썬 코드를 만들고 해당 쿼리문을 적용하여 pw 를 구하였다.

<img width="563" alt="스크린샷 2020-01-06 오후 6 42 51" src="https://user-images.githubusercontent.com/54495632/71819341-f7fa6580-30ce-11ea-9c21-f0f0c43f5796.png">


<img width="415" alt="스크린샷 2020-01-06 오후 8 53 55" src="https://user-images.githubusercontent.com/54495632/71819274-bec1f580-30ce-11ea-85e5-812e09c5c75a.png">


?! login fail 이 나왔다.

<img width="553" alt="스크린샷 2020-01-06 오후 8 56 37" src="https://user-images.githubusercontent.com/54495632/71819358-05afeb00-30cf-11ea-9538-3258a26af6e6.png">

파이썬 코드의 중첩문에서 두 번째 중첩문을

for j in range(127,90,-1): 와 같이 반대로 했더니 다른 값이 나왔다.

db 상 쿼리 접근을 잘못했나 싶긴한데

is_no_rest~ 이 부분 부터 같은 것으로 보아 admin 외에 다른 pw 가 존재하여

오류가 발생한 것 같다. id = guest pw =guest 인 아이디가 존재하고

앞에서 부터 쿼리를 던졌을 때와 뒤에서 부터 진행할 때의 결과가 다른 것 같다.

두 개의 결과를 비교하여 guest , pw 가 there_is_no_rest_for_the_white_angel

을 유추하였고


<img width="445" alt="스크린샷 2020-01-06 오후 8 54 26" src="https://user-images.githubusercontent.com/54495632/71819364-0b0d3580-30cf-11ea-900c-3cf24ec81c13.png">



<img width="390" alt="스크린샷 2020-01-06 오후 8 54 32" src="https://user-images.githubusercontent.com/54495632/71819372-11031680-30cf-11ea-968f-54ada32e7c02.png">

해결하였다. 원래 문제가 id 두 개랑 pw 두 개를 파이썬 코드로 쉽게 구하는 것 같은데

id 를 admin 으로 예상하여 쿼리문을 던진 거라 관련 코드를 다시 한 번 작성해봐야겠다.
