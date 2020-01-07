<img width="280" alt="스크린샷 2020-01-07 오후 9 15 55" src="https://user-images.githubusercontent.com/54495632/71894931-fdb97f00-3192-11ea-8418-379641ad0010.png">

43번

<img width="388" alt="스크린샷 2020-01-07 오후 9 16 52" src="https://user-images.githubusercontent.com/54495632/71895122-846e5c00-3193-11ea-8352-bc7c644a4712.png">

웹쉘을 업로드해 cat /flag 를 실행하면 되는 문제인 것 같다.

<img width="388" alt="스크린샷 2020-01-07 오후 9 16 52" src="https://user-images.githubusercontent.com/54495632/71896007-eaf47980-3195-11ea-862e-222eaf7d656f.png">

<img width="308" alt="스크린샷 2020-01-07 오후 9 21 09" src="https://user-images.githubusercontent.com/54495632/71896008-ec25a680-3195-11ea-81e1-c6a5350a90d0.png">

그 전에 사용했던 아무 확장자 없는 파일을 올리니 거부된다.

<img width="330" alt="스크린샷 2020-01-07 오후 9 20 58" src="https://user-images.githubusercontent.com/54495632/71896048-019ad080-3196-11ea-8207-f9ebb9cbbbf4.png">

아무 .png 이미지 파일을 올리니 해당 파일은 맞게 업로드가 됐다.

<img width="484" alt="스크린샷 2020-01-07 오후 9 22 23" src="https://user-images.githubusercontent.com/54495632/71896139-37d85000-3196-11ea-8478-3541a73fe832.png">

cat /flag를 실행시켜줄 php 형식의 파일을 터미널로 생성하고 업로드를 해보았다.

<img width="440" alt="스크린샷 2020-01-07 오후 9 23 41" src="https://user-images.githubusercontent.com/54495632/71896161-4c1c4d00-3196-11ea-9d51-152afbf31b49.png">

는 거부당했다 ㅠ ... 아마도 여러 파일 형식에 대한 필터링 조건이 따로 있는듯 하다.

<img width="720" alt="스크린샷 2020-01-07 오후 9 58 07" src="https://user-images.githubusercontent.com/54495632/71897095-e5e4f980-3198-11ea-8a59-a8d494aa81e6.png">

Burp Suite 프로그램에서 프록시로 해당 파일들을 확인 했다. 아무 png 스크린샷 파일을 확인 했을 

때, Content-Type 은 image/png 형식이다.

<img width="486" alt="스크린샷 2020-01-07 오후 9 57 48" src="https://user-images.githubusercontent.com/54495632/71897164-1af14c00-3199-11ea-97df-6a6141ed3cfd.png">

php 파일 형식이 text/php이고 이를  image/png 형식으로 변경하였다.

<img width="500" alt="스크린샷 2020-01-07 오후 9 58 16" src="https://user-images.githubusercontent.com/54495632/71897168-1e84d300-3199-11ea-8e97-f50464b46eb3.png">

그 후 burp-suite 의 forward 를 통해 해당 정보를 전달하여

<img width="331" alt="스크린샷 2020-01-07 오후 9 55 03" src="https://user-images.githubusercontent.com/54495632/71897238-52f88f00-3199-11ea-8270-a3bee7b3e40f.png">

<img width="512" alt="스크린샷 2020-01-07 오후 9 55 13" src="https://user-images.githubusercontent.com/54495632/71897242-5724ac80-3199-11ea-93e2-ef7d68d38b6e.png">

다음과 같은 FLAG 를 얻을 수 있었다.

<img width="436" alt="스크린샷 2020-01-07 오후 10 02 45" src="https://user-images.githubusercontent.com/54495632/71897289-791e2f00-3199-11ea-92b9-61c36484c6dd.png">

 