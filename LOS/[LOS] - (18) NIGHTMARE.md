# Los 18 NightMare

<img width="225" alt="스크린샷 2020-01-29 오후 8 46 32" src="https://user-images.githubusercontent.com/54495632/73355981-a2cfff00-42dc-11ea-9c3e-13d44d34c202.png">

<img width="730" alt="스크린샷 2020-01-29 오후 8 46 39" src="https://user-images.githubusercontent.com/54495632/73355996-a9f70d00-42dc-11ea-86a0-c0feb6a326d3.png">

18번



## 필터링 조건

```php
if(preg_match('/prob|_|\.|\(\)|#|-/i', $_GET[pw])) exit("No Hack ~_~"); 
if(strlen($_GET[pw])>6) exit("No Hack ~_~"); 
```

preg_match 함수에 의해 # , -- 주석처리는 불가능하게 된다.
strlen($_GET[pw]>6) 이므로 pw 로 받는 string 길이가 6 이 넘어가면 필터링 되어 No Hack ~_~ 이 출력될 것이다.

주석 우회로는
/**/
;%00 등이 가능하다.






## 쿼리

```php
$query = "select id from prob_nightmare where pw=('{$_GET[pw]}') and id!='admin'"; 
```

전 문제들과는 또 새로운 쿼리문이다.
pw 가 ('') 형태이고
뒤에 id는 id!='admin' 이다.
pw에는 위에 필터링 조건과 같이 6자리를 넘기면 안된다.

여기서 생각했던 것은 where 문 조건 중 pw를 TRUE 로 만들고
나머지 and 이후 절은 주석 처리 하여 전체 WHERE 절을 TRUE로 만드는 것이였다.

하지만 주석에 있어 %23 즉 # 은 위 preg_match 함수에 의해 필터링되어 불가능 했다. -> /**/ 나 ;%00 이용

pw=('') 에서 아무것도 입력되지 않으면 ('') 자체는 FALSE 가 된다.
FALSE = FALSE -> 이와 같은 조건을 주게 되면 전체가 TRUE가 된다.

pw=('') = 0 -> pw=TRUE
그 뒤에 주석 처리를 해줘야됐다.





## 결과


<img width="744" alt="스크린샷 2020-01-29 오후 10 18 57" src="https://user-images.githubusercontent.com/54495632/73360015-681e9480-42e5-11ea-8abc-95c9e83d88e2.png">


다음과 같이 주석을 /**/ 로 우회하는 경우 전체 pw 길이가 6이 넘어 필터링 된다.

<img width="714" alt="스크린샷 2020-01-29 오후 9 38 09" src="https://user-images.githubusercontent.com/54495632/73360045-74a2ed00-42e5-11ea-88d2-27c30707885d.png">


;%00 으로 나머지 뒷 부분을 주석 처리하여 문제를 해결했다.