# NAVER day1






## NAVER cafe

### 시도 목록

- 카페명
- 카페 검색
- 카페 게시글 제목
- 카페 댓글
- 카페 내부 이벤트
- 카페 채팅
- URL을 통한 접근






### 카페명

<img width="588" alt="스크린샷 2020-02-05 오후 4 30 05" src="https://user-images.githubusercontent.com/54495632/73838680-96f1b900-4857-11ea-9718-377b71d3c8b4.png">

카페명으로``` <ScR<script>iPt>alert(1);</ScR<script>iPt>``` 를 입력했으나
```<ScR<script>iPt>alert(1);</ScR< ``` 으로 나옴


<img width="476" alt="스크린샷 2020-02-05 오후 9 03 59" src="https://user-images.githubusercontent.com/54495632/73840229-0d43ea80-485b-11ea-88e0-2958a8485075.png">

여러 개의 카페명으로 시도를 해봤으나 자동으로 필터링되는듯 하다.





### 카페 검색

<img width="864" alt="스크린샷 2020-02-05 오후 4 35 13" src="https://user-images.githubusercontent.com/54495632/73839663-e20ccb80-4859-11ea-8d5b-89307a7e8675.png">

카페 검색창에 검색했을 때 <scrip 까지는 < 괄호에 이상이 없으나 <script 부터 
< 괄호가 &lt; 로 필터링된다는 것을 발견






### 카페 게시글 제목

<img width="513" alt="스크린샷 2020-02-05 오후 9 11 17" src="https://user-images.githubusercontent.com/54495632/73841403-e5a25180-485d-11ea-875d-332fab0da82f.png">

원래의 입력값으로 나오나 실행은 되지 않는듯 하다.








### 카페 댓글

<img width="439" alt="스크린샷 2020-02-05 오후 9 11 25" src="https://user-images.githubusercontent.com/54495632/73841463-0ff40f00-485e-11ea-8a9a-14ee8e9c7e90.png">

여러 시도 중 일부만 가져왔는데 < 괄호 자체가 다 필터링 되는 것 같다...





### 카페 내부 이벤트

이벤트 설정 저장 전
<img width="948" alt="스크린샷 2020-02-05 오후 5 20 34" src="https://user-images.githubusercontent.com/54495632/73841740-94df2880-485e-11ea-9e4a-e7db8982a931.png">


설정 저장 후

<img width="899" alt="스크린샷 2020-02-05 오후 5 21 36" src="https://user-images.githubusercontent.com/54495632/73841758-9d376380-485e-11ea-9487-7165c6615c5b.png">

<img width="871" alt="스크린샷 2020-02-05 오후 5 38 20" src="https://user-images.githubusercontent.com/54495632/73841838-c0faa980-485e-11ea-9c25-031fec87f6b2.png">


< 괄호가 역시나 필터링 된다. 
해당되는 이벤트 발생 시 (위에 카페 게시글 글만 스크린샷) 글만 새로 생성되고 따로 xss가 발생하진 않는다.





### 카페 채팅

<img width="1667" alt="스크린샷 2020-02-05 오후 9 35 16" src="https://user-images.githubusercontent.com/54495632/73842195-72014400-485f-11ea-8628-62072434dc43.png">


<img width="1190" alt="스크린샷 2020-02-05 오후 9 35 24" src="https://user-images.githubusercontent.com/54495632/73842204-762d6180-485f-11ea-8c57-f1e31e9955e9.png">

카페라는 플랫폼안에 여러 기능이 있어 기본적인 xss이 뚫린 곳이 있을 수도 있지 않을까 싶었지만 가능한 곳이 없었다 .





### URL 접근

불가능
<img width="1068" alt="스크린샷 2020-02-05 오후 9 57 01" src="https://user-images.githubusercontent.com/54495632/73853757-bea34a00-4874-11ea-9bb4-6b46a5149faa.png">