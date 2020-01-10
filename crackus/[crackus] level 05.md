<img width="150" alt="스크린샷 2020-01-10 오후 4 32 52" src="https://user-images.githubusercontent.com/54495632/72134257-e662d780-33c6-11ea-9360-181d8aa17189.png">

LV4.

<img width="655" alt="스크린샷 2020-01-10 오후 4 32 56" src="https://user-images.githubusercontent.com/54495632/72134266-ee227c00-33c6-11ea-84bd-1b94d9fec599.png">
<img width="478" alt="스크린샷 2020-01-10 오후 4 33 00" src="https://user-images.githubusercontent.com/54495632/72134270-efec3f80-33c6-11ea-8c16-d44401db1aaf.png">

해당 문제 소스코드와 쿼리이다. 다른 문제와 다르게 일단 id 만 TRUE 를 만들어 주면 될 것 같다.

if(preg_match('/play|_|\.|\(|\)|info/i', $id)){ exit("Nope !!");}
 if(preg_match('/or|admin|#/i', $id)){ exit("Query is filtered :( ");}

preg_match 함수에 의해 or, admin, # 사용이 필터링 되고 있으며
id =admin 으로 로그인을 하면 다음 레벨로 갈 수 있다.

admin 자체가 필터링 되고 있으므로 %, 와 _ 으로 admin에서 특정 부분의 문자를 대치 하는 방법이 존재했다. like 도 같이 이용했다.

퀴리를 SELECT ID FROM play_sql05 where id=' ' || id like 'ad%in' 으로 주어 해결했다.
ad%in 으로 주게 되면 admin 이라는 필터링 조건을 피할 수 있다.
%는 한 글자 이상의 문자열을 대신할 수 있다. _는 한글자만 가능하다.

<img width="481" alt="스크린샷 2020-01-10 오후 4 53 43" src="https://user-images.githubusercontent.com/54495632/72135547-13fd5000-33ca-11ea-9478-1909c56764c6.png">

URL 은 다음과 같이 주었고 해결했다.

<img width="770" alt="스크린샷 2020-01-10 오후 4 53 48" src="https://user-images.githubusercontent.com/54495632/72135556-1c558b00-33ca-11ea-854e-073827a55e3d.png">

Concat이라는 함수를 이용해서 푸는 방법도 존재한다.

Concat(값1,값2,.... , 값n ) 하게 되면 값1~값n 까지 합쳐진 문자열이 나열되게 된다.
즉 , Concat('a','dmi','n') 과 같은 형태를 만들면 admin 의 필터링에 걸리지 않고 admin을 사용할 수 있다.

<img width="870" alt="스크린샷 2020-01-10 오후 5 36 02" src="https://user-images.githubusercontent.com/54495632/72138216-b7049880-33cf-11ea-89d1-73b81f82fc3b.png">

<img width="903" alt="스크린샷 2020-01-10 오후 5 37 03" src="https://user-images.githubusercontent.com/54495632/72138331-f92dda00-33cf-11ea-8f93-ddc6d43bf367.png">
<img width="830" alt="스크린샷 2020-01-10 오후 5 38 02" src="https://user-images.githubusercontent.com/54495632/72138339-fb903400-33cf-11ea-9c34-55f3cb57c1c3.png">

또한 , 다음과 같이 admin 을 hex로 0x61646d696e 로 주거나
char 함수를 이용하여 char(97,100,109,105,110) 와 같이 admin을 만드는 방법도 가능하다.