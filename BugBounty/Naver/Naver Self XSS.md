# NAVER SELF XSS

네이버에서 발생할 수 있는 self XSS를 정리했습니다.

버그 바운티 범위안에 포함되지 않습니다.




## NAVER Cafe

<img width="1002" alt="스크린샷 2020-02-16 오후 4 16 10" src="https://user-images.githubusercontent.com/54495632/74600687-4b050680-50d8-11ea-9bcd-e3584d9c3beb.png">

카페 대문 에디터에서 html 설정을 클릭한 후 해당 부분에 
XSS 공격 구문을 작성한 후 html 설정 해제

<img width="1026" alt="스크린샷 2020-02-16 오후 4 16 22" src="https://user-images.githubusercontent.com/54495632/74600708-ac2cda00-50d8-11ea-97d3-d644d4409e28.png">

의도했던 XSS 가 발생하나 self XSS 이다.

<img width="954" alt="스크린샷 2020-02-16 오후 4 22 28" src="https://user-images.githubusercontent.com/54495632/74600716-bfd84080-50d8-11ea-93e5-6f6b31b05367.png">

해당 과정을 반대로 하면 (html 체크 없이 XSS 시도 -> html 설정)
< > 꺽쇠괄호가 &gt; , &lt; 로 필터링 된다는 것을 알 수 있다.



## NAVER Blog




### Html 설정을 이용한 self XSS

<img width="1083" alt="스크린샷 2020-02-16 오후 4 16 54" src="https://user-images.githubusercontent.com/54495632/74600737-f57d2980-50d8-11ea-8fae-90b68a84e5c8.png">
<img width="1047" alt="스크린샷 2020-02-16 오후 4 17 03" src="https://user-images.githubusercontent.com/54495632/74600739-fa41dd80-50d8-11ea-906f-65844379292a.png">

기본적인 과정이 Cafe에서 진행했던 self Xss와 같다.






### 블로그-> 글쓰기 -> 글장식 -> 요리 이용한 Self XSS

<img width="1040" alt="스크린샷 2020-02-16 오후 4 29 44" src="https://user-images.githubusercontent.com/54495632/74600806-ffebf300-50d9-11ea-9bda-9b5232106700.png">

다음과 같은 네이버 블로그 글쓰기에서 글장식 -> 요리 선택

<img width="549" alt="스크린샷 2020-02-16 오후 4 30 03" src="https://user-images.githubusercontent.com/54495632/74600820-1abe6780-50da-11ea-912a-33bd3b19b218.png">

원하는 XSS 공격을 입력한 후 적용

<img width="785" alt="스크린샷 2020-02-16 오후 4 30 14" src="https://user-images.githubusercontent.com/54495632/74600825-2ad64700-50da-11ea-8979-eb724abfc77c.png">

작성된 글 자체에서는 따로 xss가 발생되지 않지만 글 수정을 누르게 되면

<img width="1087" alt="스크린샷 2020-02-16 오후 4 30 21" src="https://user-images.githubusercontent.com/54495632/74600834-404b7100-50da-11ea-8d3b-56e0bae5c447.png">
<img width="1680" alt="스크린샷 2020-02-16 오후 4 30 30" src="https://user-images.githubusercontent.com/54495632/74600835-43def800-50da-11ea-9916-93e245ddbbe4.png">


다음과 같이 self XSS 가 발생하게 된다.

이를 활용하여 <script> 태그 이외에 다른 태그를 이용하는 것도 가능하다.

<img width="1341" alt="스크린샷 2020-02-16 오후 5 23 39" src="https://user-images.githubusercontent.com/54495632/74601379-1c3f5e00-50e1-11ea-86e7-03a2a27fb4a4.png">

<div> 태그 이용

<img width="1189" alt="스크린샷 2020-02-16 오후 5 24 14" src="https://user-images.githubusercontent.com/54495632/74601385-2b261080-50e1-11ea-83a8-084b70de54de.png">

<img> 태그 이용

<img width="839" alt="스크린샷 2020-02-16 오후 5 23 11" src="https://user-images.githubusercontent.com/54495632/74601390-34af7880-50e1-11ea-860a-9eb50433a8ae.png">

글쓰기에서만 적용 가능하고 서버에 해당 이미지를 저장 하는 부분에서 동작이 안된다.





### Blog 프로필 self XSS


- URL 입력

<img width="829" alt="스크린샷 2020-02-16 오후 6 18 33" src="https://user-images.githubusercontent.com/54495632/74602120-f918ac80-50e8-11ea-818e-6d0b46b51fd1.png">
<img width="927" alt="스크린샷 2020-02-16 오후 6 18 41" src="https://user-images.githubusercontent.com/54495632/74602123-fd44ca00-50e8-11ea-8fb0-db6fc9c1fa72.png">

다음과 같이 URL 입력을 한 후 해당 XSS 가 실행되지만 글 작성시



<img width="949" alt="스크린샷 2020-02-16 오후 6 19 10" src="https://user-images.githubusercontent.com/54495632/74602131-0afa4f80-50e9-11ea-9447-5efc4b488183.png">



아무 반응이 없으며



<img width="696" alt="스크린샷 2020-02-16 오후 6 19 24" src="https://user-images.githubusercontent.com/54495632/74602133-0f266d00-50e9-11ea-8e78-05789379e92f.png">



삽입했던 해당 공격이 필터링된 것을 알 수 있다.


- 동영상 업로드

<img width="416" alt="스크린샷 2020-02-16 오후 6 32 33" src="https://user-images.githubusercontent.com/54495632/74604072-cf1db500-50fd-11ea-8f6f-1f7cfa6d8dee.png">


다음과 같이 입력하여 xss 를  띄우는 것이 가능하다.

<img width="1083" alt="스크린샷 2020-02-16 오후 6 22 45" src="https://user-images.githubusercontent.com/54495632/74604076-d93fb380-50fd-11ea-9f65-a5acfeb646b2.png">

URL로 입력값을 미리 넣고 미리보기를 실행할 수 있다면 
reflected XSS로도 볼 수 있는 취약점이지만 불가능한 것 같고
self XSS로 보기에도 애매하다...
