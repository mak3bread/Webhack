<img width="165" alt="스크린샷 2020-01-16 오후 8 28 39" src="https://user-images.githubusercontent.com/54495632/72521664-321df100-389f-11ea-9c58-949371451f63.png">

9번 VAMPIRE

<img width="535" alt="스크린샷 2020-01-16 오후 8 28 57" src="https://user-images.githubusercontent.com/54495632/72521761-67c2da00-389f-11ea-9808-f91816b3e20d.png">


if(preg_match('/\'/i', $_GET[id])) exit("No Hack ~_~");
$_GET[id] = strtolower($_GET[id]);
$_GET[id] = str_replace("admin","",$_GET[id]);

preg_match 함수에 의해 ' 작은 따옴표가 필터링되고
get으로 id를 입력하면 strtolower에 의해 이전 문제 처럼 대문자를 입력하면
소문자로 변경된다.

str_replace 함수로 admin -> null 처리된다.

이 문제에선 str_replace 함수를 이용해서 문제를 풀었다.

admin -> ""로 처리 되므로
id=aadmindmin 을 입력하게 되면 중간의 admin ->"" 처리되어
결국 id=admin 이 남게된다.

입력은 admin 문자열 사이 위치 아무 곳에나  연속된 admin을 입력하면 된다.

<img width="738" alt="스크린샷 2020-01-16 오후 8 44 01" src="https://user-images.githubusercontent.com/54495632/72522609-71e5d800-38a1-11ea-8668-083d56ad44dc.png">