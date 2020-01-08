![img](https://k.kakaocdn.net/dn/dLRwN9/btqAQlo3Wpj/4pRqklRRpVbm004qBUm38k/img.png)



 

webhacking.kr 문제를 지속적으로 풀다가 

SQL Injection을 따로 다루어야할 필요성을 느껴 시작했다.

 



![img](https://k.kakaocdn.net/dn/2No39/btqAQOYSo8z/SkUDFGqJWSVgdLMHtaWpok/img.png)



 

preg_match로 필터링을 주었고

 

prob _ . 등 필터링이 된다.

 

id 와 pw 가 맞도록 SQL injection을 시도하였다.

 



![img](https://k.kakaocdn.net/dn/DylxA/btqAQNM5xOO/H7CkZ1NwxWQjGbxKr7uZR0/img.png)



id 에 admin을 주고 

url로 %23 과 %27를 넣어

\# ' 를 표현했다.

\#는 id=admin' 뒤로 주석처리를 의미한다.

 



![img](https://k.kakaocdn.net/dn/QLHQ6/btqASzNIWAY/4d365p7uKJkbx1nWLRQZs0/img.png)



 

id=admin&pw=1' or '1' = '1 와 같은 풀이도 가능하다.

 

해당 데이터 베이스에 1이라는 id 와 admin 이라는 값이 있어서 가능했다.

 

id에 1과 admin을 주고 pw를 주석이나 1' or '1' = '1 로 true가 나오게끔 하여

 

문제를 해결하였다.