![img](https://k.kakaocdn.net/dn/LYM1I/btqAUuSGobt/Oi7mzggoU3Kd70oWrKo550/img.png)



 

3번 고블린

 



![img](https://k.kakaocdn.net/dn/b0Fvby/btqAQOFhuIU/Mori4BnLEaawfKHOfciFKK/img.png)



if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~");

 

if(preg_match('/\'|\"|\`/i', $_GET[no])) exit("No Quotes ~_~"); 

 

전의 preg_match 에 의해 필터링 되는 조건에서 몇 가지 더 추가 됐다.

 

' " 등 필터링된다.

 

쿼리문 자체는 이미 id 에 =guest 가 입력되어 있고 no = 값을 입력되는 구조이다.

 



![img](https://k.kakaocdn.net/dn/bQ65pH/btqATf2vR4B/g9k53VohlsTBc1PnawuS11/img.png)



 

no 에 1를 입력하니 Hello guest 가 나왔다.

 

우연히 guest의 no 값을 찾았고

 

1이 아닌 다른 값을 넣어주면

 



![img](https://k.kakaocdn.net/dn/ctvbXn/btqARyodLlh/bBNARoMuyTGfnh6hNx3Qfk/img.png)



 

Hello guest가 나오지 않는다.

 

이를 이용하고 필터링 조건을 고려하여

 

id = 'guest' and no ='1이 아닌 값'  -> 여긴 false

or

id = 'admin'  -> true 

 

와 같은 구조로 해결하기로 했다.

 



![img](https://k.kakaocdn.net/dn/bBsXFh/btqAQNM7fMA/Wr46x8jKlFBb851Ns57l0k/img.png)



no hack 이 아닌 no Quotes 가 나온 것을 보니 

 

%27 도 필터링이 되는 것 같다.

 



![img](https://k.kakaocdn.net/dn/OGjUl/btqARh1iQ8z/JBVmoclM7kLVx4kW9L5y41/img.png)



 

admin 값 자체를 

char( 아스키 코드 값) 형태로 주었더니 해결이 됐다.

a - 97

d - 100

m - 109

i - 105

n - 110

 



![img](https://k.kakaocdn.net/dn/pPAf9/btqAUukOKAr/hECg6HbF2nFRwSGohcxAXk/img.png)



 

또 여러 가지 시도를 해보았는데, 해당 문제의 데이터 베이스 구조가

 

id    no

guest  1

admin  2

 

로 구성되어 있어

 

no=2 or no!=1 로도 해결할 수 있다.