<img width="278" alt="스크린샷 2020-01-07 오후 10 08 08" src="https://user-images.githubusercontent.com/54495632/71898144-ec28a500-319b-11ea-97bb-71fe80751dc0.png">

51번

<img width="806" alt="스크린샷 2020-01-07 오후 10 08 20" src="https://user-images.githubusercontent.com/54495632/71898152-ef239580-319b-11ea-9e6f-16d1cca30627.png">

인젝션 같다 뭔가.. 소스코드를 보자

<img width="965" alt="스크린샷 2020-01-07 오후 10 08 33" src="https://user-images.githubusercontent.com/54495632/71898164-f64aa380-319b-11ea-968f-18cfc13ad99b.png">

id 부분에서 addslashes() 함수는 넘겨준 문자열 안에 ' " \ NULL 등이 있으면 해당 문자 앞에 

\ 역슬래시를 추가해주는 함수이다.

pw 부분에서 md5 함수에서 첫 부분은 pw의 string 이고 두 번째 파라미터엔 True 나 false 가 입력 

될 수 있는데 값이 true 인 경우 해시 길이 16bit binary 형식으로 변환하고 false 나 생략인 경우 

default 처리가 된다.(hex 값)

md5의 취약점 중 '=' 문자열이 나오는 경우 'abc' = 'def' 와 같이 나오면 

false injection이 가능해진다.

<img width="384" alt="스크린샷 2020-01-07 오후 11 48 01" src="https://user-images.githubusercontent.com/54495632/71904209-12087680-31a9-11ea-9822-ddbdc3098ada.png">

php 상에서 pw 암호를 구하는 것이 가능하겠지만 파이썬의 hashlib 를 이용하여

비밀번호를 따로 구하였다.

<img width="276" alt="스크린샷 2020-01-07 오후 11 30 06" src="https://user-images.githubusercontent.com/54495632/71904258-29476400-31a9-11ea-81ec-6614ebc25589.png">

<img width="447" alt="스크린샷 2020-01-07 오후 11 47 52" src="https://user-images.githubusercontent.com/54495632/71904276-2b112780-31a9-11ea-9ca7-34598b4b3c19.png">