![img](https://k.kakaocdn.net/dn/bajDcC/btqARyPl7Yl/ffftHTXiKrX9pBBjFre5q0/img.png)



코볼트 .. 문제 이름이 몬스터 이름인 것 같다.

 



![img](https://k.kakaocdn.net/dn/8NCFz/btqASyafwwh/wCLy60bkzBamr4dmvK2u11/img.png)



문제 해결 자체는 gremlin 과 차이가 없다.

소스코드를 좀 더 보면

 

preg_match 로  prob  _ .  \ 등이 걸러진다.

 

쿼리문을 보니 id 와 pw 를 넣는데 id는 그대로 들어가고 pw에서 md5 해싱이 된 값? 을 넣는 구조라는 것을 알 수 있다.

 

소스 코드 중

if($result['id'] == 'admin') solve("cobolt");

을 보면 앞 문제 gremlin 과는 다르게 id 가 admin 여야 한다는 것을 알 수 있다.

 



![img](https://k.kakaocdn.net/dn/cUzv2N/btqARXVB2TY/46mXmerArexDkhBjjxQTh1/img.png)



 

구조 자체는 

id = admin'# 

\#를 주어 뒤에 패스워드 쪽을 주석처리했다.

URL 로 변경하여  ' - > %27 , # -> %23 처리 하였다.
