<img width="289" alt="스크린샷 2020-01-14 오후 2 02 01" src="https://user-images.githubusercontent.com/54495632/72315985-11576f00-36d8-11ea-9fd7-98af8f982386.png">

3번

<img width="534" alt="스크린샷 2020-01-14 오후 2 02 13" src="https://user-images.githubusercontent.com/54495632/72315995-14eaf600-36d8-11ea-8063-31145dc9172b.png">

퍼즐이 있다..
오른쪽 아래 5X5 칸을 누르면 흰색 ->검정색으로 변하며
3,5 -> 연속
1,1,1 이런 식은 합이 같으면 된다는 형식으로 생각하고 눌러봤다.

<img width="590" alt="스크린샷 2020-01-14 오후 2 08 03" src="https://user-images.githubusercontent.com/54495632/72316206-c12cdc80-36d8-11ea-8bca-85e949e195d8.png">

<img width="785" alt="스크린샷 2020-01-14 오후 2 08 18" src="https://user-images.githubusercontent.com/54495632/72316327-24b70a00-36d9-11ea-8356-a987af1ab120.png">

clear?!
log in 할 이름을 입력하라고 해서 당연히 admin으로 접속했다.

<img width="347" alt="스크린샷 2020-01-14 오후 2 08 36" src="https://user-images.githubusercontent.com/54495632/72316368-43b59c00-36d9-11ea-8c3d-857e64231130.png">

입력한 admin , answer , ip 값이 나왔다.
여기서 name과 ip 는 내가 입력한 name값과 내 아이피 값이고
answer은 뭔지 잘 몰랐으나 아까전 name 입력칸으로 가니

URL이 다음과 같이 나와있었다.
_1=1&_2=0&_3=1&_4=0&_5=1&_6=0&_7=0&_8=0&_9=0&_10=0&_11=0&_12=1&_13=1&_14=1&_15=0&_16=0&_17=1&_18=0&_19=1&_20=0&_21=1&_22=1&_23=1&_24=1&_25=1&_answer=1010100000011100101011111

아까 전 5 x 5 행렬? 을 1~25 까지 나타냈을 때 검은색 칸이 1이 되는 것 같다.

<img width="331" alt="스크린샷 2020-01-14 오후 2 30 04" src="https://user-images.githubusercontent.com/54495632/72317249-f686f980-36db-11ea-90cc-420ded20793c.png">

name 을 통한 injection은 동작하지 않는다.

<img width="329" alt="스크린샷 2020-01-14 오후 2 38 57" src="https://user-images.githubusercontent.com/54495632/72317133-a019bb00-36db-11ea-9763-1e667936ac27.png">

소스 코드를 열어 다음과 같이 SQL Injection 을 시도한 뒤
name 에 admin을 주면

<img width="476" alt="스크린샷 2020-01-14 오후 2 38 12" src="https://user-images.githubusercontent.com/54495632/72317166-b889d580-36db-11ea-9e8b-c2983d86d25d.png">