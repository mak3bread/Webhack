<img width="286" alt="스크린샷 2020-01-08 오후 5 29 31" src="https://user-images.githubusercontent.com/54495632/71962308-7e808580-323c-11ea-891b-4dd28d792d7c.png">

4번

<img width="415" alt="스크린샷 2020-01-08 오후 5 29 44" src="https://user-images.githubusercontent.com/54495632/71962317-850efd00-323c-11ea-903c-6ef6cc23b203.png">

무언가 해싱된 듯한 값이 나와있고 password 를 제출하는 칸이 따로 있었다.

소스코드를 보자.

<img width="887" alt="스크린샷 2020-01-08 오후 5 29 52" src="https://user-images.githubusercontent.com/54495632/71962725-7117cb00-323d-11ea-8b38-c89682d0ef61.png">

$hash 가 rand() 함수로 인해 8자리 랜덤 값을 가지고 뒤에 salt_for_you 라는 문자열이 추가된다.

$_Session['chall4'] 를 $hash 로 assign 한다.

for문에 의해 $hash 가 sha1으로 500 번 해싱된다.

따라서, 8자리의 문자열 + salt_for_you 라는 문자열을 500 번 sha1 해싱한 값이 처음 화면에 나타난다는

의미인데... 8자리 * 500번 해싱이면 컴퓨터에 무리가 많이 갈 것 같다. 파이썬에 sha1 와 hashlib 라이브러리가 있어

구하는 방법 자체는 간단하지만 성능이 너무 안좋다. 코드를 실행시키고 밥을 먹고 오거나 다른 할 일을 하는 것을 추천

더 효율적으로 하기 위해서는 언어를 파이썬외에 다른 언어로 sha1 를 구현하던가 파이썬에서 파일로 

여러 분할 하여 저장해서 찾는 방법도 가능할 것 같다.

화면에 나온 해싱된 값과 비교하는 방법을 사용하게 되면 중간에 webhacking.kr 사이트의 로그인이 끊기는 경우가 

있어서 10000000 부터 99999999 + salt_for_you 를 500 해싱한 값들을 파일에 저장하고 찾기로 결정했다.

<img width="748" alt="스크린샷 2020-01-08 오후 9 31 57" src="https://user-images.githubusercontent.com/54495632/71978504-dd56f680-325e-11ea-9dc2-30bf957e6e18.png">

10000000 부터 99999999 까지의 해싱정보를 파일로 제작하는것 자체도 너무 오래걸려 

10000000 부터 20000000 까지만 해싱한 파일을 따로 저장하여

4번문제 첫 화면에서 나오는 해싱값을 계속 새로 고침하여 visual studio 코드를 통해 찾았다.

<img width="404" alt="스크린샷 2020-01-08 오후 9 32 33" src="https://user-images.githubusercontent.com/54495632/71978801-8dc4fa80-325f-11ea-92d6-d4450325839c.png">

중간에 t 가 빠졌다. 아무튼 8자리 + salt_for_you 인 답을 입력하면

<img width="448" alt="스크린샷 2020-01-08 오후 9 33 59" src="https://user-images.githubusercontent.com/54495632/71978845-a59c7e80-325f-11ea-8759-5a4bb9c0f972.png">

<img width="417" alt="스크린샷 2020-01-08 오후 9 34 04" src="https://user-images.githubusercontent.com/54495632/71978849-a7fed880-325f-11ea-8930-6fd68124be75.png">

좀 더 빠른 언어나 파이썬에서의 다른 해결책을 찾아봐야겠다.

<img width="286" alt="스크린샷 2020-01-08 오후 5 29 31" src="https://user-images.githubusercontent.com/54495632/71962308-7e808580-323c-11ea-891b-4dd28d792d7c.png">

4번

<img width="415" alt="스크린샷 2020-01-08 오후 5 29 44" src="https://user-images.githubusercontent.com/54495632/71962317-850efd00-323c-11ea-903c-6ef6cc23b203.png">

무언가 해싱된 듯한 값이 나와있고 password 를 제출하는 칸이 따로 있었다.

소스코드를 보자.

<img width="887" alt="스크린샷 2020-01-08 오후 5 29 52" src="https://user-images.githubusercontent.com/54495632/71962725-7117cb00-323d-11ea-8b38-c89682d0ef61.png">

$hash 가 rand() 함수로 인해 8자리 랜덤 값을 가지고 뒤에 salt_for_you 라는 문자열이 추가된다.

$_Session['chall4'] 를 $hash 로 assign 한다.

for문에 의해 $hash 가 sha1으로 500 번 해싱된다.

따라서, 8자리의 문자열 + salt_for_you 라는 문자열을 500 번 sha1 해싱한 값이 처음 화면에 나타난다는

의미인데... 8자리 * 500번 해싱이면 컴퓨터에 무리가 많이 갈 것 같다. 파이썬에 sha1 와 hashlib 라이브러리가 있어

구하는 방법 자체는 간단하지만 성능이 너무 안좋다. 코드를 실행시키고 밥을 먹고 오거나 다른 할 일을 하는 것을 추천

더 효율적으로 하기 위해서는 언어를 파이썬외에 다른 언어로 sha1 를 구현하던가 파이썬에서 파일로 

여러 분할 하여 저장해서 찾는 방법도 가능할 것 같다.

화면에 나온 해싱된 값과 비교하는 방법을 사용하게 되면 중간에 webhacking.kr 사이트의 로그인이 끊기는 경우가 

있어서 10000000 부터 99999999 + salt_for_you 를 500 해싱한 값들을 파일에 저장하고 찾기로 결정했다.

<img width="748" alt="스크린샷 2020-01-08 오후 9 31 57" src="https://user-images.githubusercontent.com/54495632/71978504-dd56f680-325e-11ea-9dc2-30bf957e6e18.png">

10000000 부터 99999999 까지의 해싱정보를 파일로 제작하는것 자체도 너무 오래걸려 

10000000 부터 20000000 까지만 해싱한 파일을 따로 저장하여

4번문제 첫 화면에서 나오는 해싱값을 계속 새로 고침하여 visual studio 코드를 통해 찾았다.

<img width="404" alt="스크린샷 2020-01-08 오후 9 32 33" src="https://user-images.githubusercontent.com/54495632/71978801-8dc4fa80-325f-11ea-92d6-d4450325839c.png">

중간에 t 가 빠졌다. 아무튼 8자리 + salt_for_you 인 답을 입력하면

<img width="448" alt="스크린샷 2020-01-08 오후 9 33 59" src="https://user-images.githubusercontent.com/54495632/71978845-a59c7e80-325f-11ea-8759-5a4bb9c0f972.png">

<img width="417" alt="스크린샷 2020-01-08 오후 9 34 04" src="https://user-images.githubusercontent.com/54495632/71978849-a7fed880-325f-11ea-8930-6fd68124be75.png">

좀 더 빠른 언어나 파이썬에서의 다른 해결책을 찾아봐야겠다.

from hashlib import sha1

f=open("list1.csv",'w')

for i in range(10000000,15000000):
    password=str(i)+"salt_for_you"

    for j in range(0,500):
        password=sha1(password.encode('utf-8')).hexdigest()


    f.write(str(i)+","+password+"\n")

f.close
