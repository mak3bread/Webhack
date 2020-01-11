<img width="152" alt="스크린샷 2020-01-11 오전 12 20 28" src="https://user-images.githubusercontent.com/54495632/72164753-a113c980-3409-11ea-8bed-48b6190a378d.png">

Lv 9.

<img width="667" alt="스크린샷 2020-01-11 오전 12 20 42" src="https://user-images.githubusercontent.com/54495632/72164770-a8d36e00-3409-11ea-8880-826309dbd91c.png">
<img width="614" alt="스크린샷 2020-01-11 오전 12 20 49" src="https://user-images.githubusercontent.com/54495632/72164777-ab35c800-3409-11ea-9d9a-3aa9a540fd04.png">

$num = $_GET['num'];
$len = $_GET['len'];
len 과 num 변수는 get형태로 받게된다.

if(!is_numeric($num) && isset($num)){ exit("Query is filtered :(");}

isset 함수는 변수가 존재하면 True를 그렇지 않으면 false를 리턴한다.
우선 num에 대한 조건은 숫자가 무조건으로 들어와야 하며 그렇지 않으면 false를 리턴한다. 또한, num 변수값이 존재해야된다.

if(preg_match('/0x/i', $num)){ exit("Query is filtered :(");}

preg_match 함수에 의해 num 값을 0x hex로 사용할 수 없다.

$query = "select * from play_sql09 where id='admin' and length(pw)>$num";

쿼리문을 보면 'admin' 행이 return 되는 상태에서 pw의 길이를 맞춰야 된다.

<img width="691" alt="스크린샷 2020-01-11 오전 12 40 30" src="https://user-images.githubusercontent.com/54495632/72165522-00bea480-340b-11ea-9030-94d37ff67a36.png">

다음과 같이 쿼리문과 부등호의 성질, 쿼리의 결과값을 통해 length값을 유추할 수 있는데
length가 0보다 커서 위의 사진에서 TRUE가 나와 Olleh ~ Admin이 출력됐다.

<img width="728" alt="스크린샷 2020-01-11 오전 12 41 58" src="https://user-images.githubusercontent.com/54495632/72165691-48453080-340b-11ea-8151-191d13e3f896.png">

<img width="695" alt="스크린샷 2020-01-11 오전 12 42 03" src="https://user-images.githubusercontent.com/54495632/72165701-4c714e00-340b-11ea-8fef-5463a95bb194.png">

<img width="701" alt="스크린샷 2020-01-11 오전 12 42 09" src="https://user-images.githubusercontent.com/54495632/72165710-509d6b80-340b-11ea-9c08-c67fc13b38de.png">

<img width="706" alt="스크린샷 2020-01-11 오전 12 42 14" src="https://user-images.githubusercontent.com/54495632/72165717-54c98900-340b-11ea-89fb-516c623b5672.png">

<img width="688" alt="스크린샷 2020-01-11 오전 12 42 22" src="https://user-images.githubusercontent.com/54495632/72165723-56934c80-340b-11ea-8ea5-148bb322477d.png">

다음과 같은 유추 과정을 통해 pw의 길이가 7임을 도출했다.

그리고 length 쿼리에서 true 를 만족하는 값을 아무거나 num=0 으로 준 뒤
and 연산자를 사용하고 len=7 을 URL로 넣었다.

<img width="495" alt="스크린샷 2020-01-11 오전 12 49 40" src="https://user-images.githubusercontent.com/54495632/72166376-70815f00-340c-11ea-91ec-193c8ccf3cfb.png">
<img width="667" alt="스크린샷 2020-01-11 오전 12 49 48" src="https://user-images.githubusercontent.com/54495632/72166380-724b2280-340c-11ea-9f49-5c8c7fd38681.png">

문제 해결!