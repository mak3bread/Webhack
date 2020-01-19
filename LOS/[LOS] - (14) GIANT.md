<img width="188" alt="스크린샷 2020-01-19 오후 7 39 12" src="https://user-images.githubusercontent.com/54495632/72679692-dea4e080-3af4-11ea-9acb-0c5bd1223597.png">



14번 Giant



<img width="559" alt="스크린샷 2020-01-19 오후 7 39 18" src="https://user-images.githubusercontent.com/54495632/72679695-e8c6df00-3af4-11ea-9c43-b85edcc2d08e.png">



공백 우회에 관한 문제이다.

$query = "select 1234 from{$_GET[shit]}prob_giant where 1";
쿼리와 사진부터 보게되면 예시로 나와있는 쿼리에서 from과 테이블 명이 붙어져 있다.
또한 where절이 이미 1로 TRUE 이다.
$shit에 공백을 받아 from과 테이블명 사이에 공간을 주면 해결되는 문제이다.

if(strlen($_GET[shit])>1) exit("No Hack ~_~"); 
shit의 길이가 1을 넘어선 안된다.
그러므로 () , /**/ 와 같은 공백을 주는 방법을 사용할 수 없다.

if(preg_match('/ |\n|\r|\t/i', $_GET[shit])) exit("HeHe"); 


공백 우회 방법으로  

Tab -> %09

Line Feed -> %0a

Vertical Tab -> %0b

Form Feed -> %0c

Carriage Return -> %0d 등이 존재한다.

위의 preg_match 에 의해 필터링 된 공백 조건은
필터링 조건 
\n - line feed
\r - carriage return
\t - tab

따라서, 사용할 수 있는 공백은 
vertical tab - %0b
form feed - %0c 등이 있다.

?shit=%0b  또는 ?shit=%0c를 통해 문제를 해결할 수 있다.



<img width="673" alt="스크린샷 2020-01-19 오후 7 48 01" src="https://user-images.githubusercontent.com/54495632/72679817-46a7f680-3af6-11ea-880c-107ceb622f78.png">

<img width="639" alt="스크린샷 2020-01-19 오후 7 48 13" src="https://user-images.githubusercontent.com/54495632/72679822-4dcf0480-3af6-11ea-8947-f297ed811fd0.png">