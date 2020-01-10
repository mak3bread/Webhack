<img width="170" alt="스크린샷 2020-01-10 오후 6 23 16" src="https://user-images.githubusercontent.com/54495632/72141497-5462cb00-33d6-11ea-9774-4304aa21db4a.png">

Lv 7.

<img width="546" alt="스크린샷 2020-01-10 오후 6 23 25" src="https://user-images.githubusercontent.com/54495632/72141513-5a58ac00-33d6-11ea-9ba2-b3551d9f16ec.png">

<img width="558" alt="스크린샷 2020-01-10 오후 6 23 22" src="https://user-images.githubusercontent.com/54495632/72141521-5c226f80-33d6-11ea-8799-fed663d1ab61.png">

쿼리문과 소스코드가 다음과 같다.

쿼리는 crackus 를 md5 한 값이 나와있고 

소스코드에서 필터링 조건들은 다음과 같다.

if(!is_numeric($hash)){ exit("Nope!!"); }
  if(preg_match('/play|_|\.|\(\)/i', $hash)){ exit("Nope !!");}
  if(preg_match('/0x/i', $hash)){ exit("Query is filtered :(");}

is_numeric(파라미터)는 매개변수가 숫자인지 판별에 주는 함수이다.

해당 매개변수가 숫자라면 is_numeric 에서 1이 반환되고 아니라면 0이 반환된다.

여기서 !is_numeric($hash)이므로 숫자가 아닌 값이 들어오면 exit 되므로

숫자만 이용해서 위 문제를 해결해야된다.

밑의 preg_match 함수에 의해서 0x 가 필터링되므로 hex 도 이용할 수 없는 상황이다.

<img width="649" alt="스크린샷 2020-01-10 오후 6 28 23" src="https://user-images.githubusercontent.com/54495632/72141911-0b5f4680-33d7-11ea-919d-98806c45bcb9.png">

crackus 를 md5로 해싱하게 되면 5045ab2f070ac272364ab275bad5873c 이다.

숫자로 시작하는 문자열의 경우 bool 값과 비교할 때

5045ab2f070ac272364ab275bad5873c 이면 5045 까지만 인식된다.

따라서 , select id from play_sql07 where md5('crackus')=5045 와 같이 쿼리문을 작성하면

해당 문제를 해결 할 수 있다.

$hash 가 GET 으로 받아지므로 ?hash=5045 로 URL를 입력하면 된다.

<img width="486" alt="스크린샷 2020-01-10 오후 6 47 37" src="https://user-images.githubusercontent.com/54495632/72143382-fa640480-33d9-11ea-9221-6031260ffb6a.png">

<img width="664" alt="스크린샷 2020-01-10 오후 6 47 45" src="https://user-images.githubusercontent.com/54495632/72143391-ff28b880-33d9-11ea-9797-5eb6e9dc61dc.png">