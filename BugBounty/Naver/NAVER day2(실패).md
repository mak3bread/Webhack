# NAVER day2 

XSS 시도



## NAVER cafe



### 시도 목록

- 카페 게시글 제목 + 내용 






### 카페 게시글 제목 + 내용 

다른 분이 취약점 발견 및 해당내용 점검
(취약점 결과 및 정보 공유 가능 여부 나오면 다시 작성)






## NAVER comic

### 시도 목록

- 웹툰 글 작성
- 웹툰 댓글 작성





### 웹툰 글 작성

제목, 내용, 웹툰 홍보에 들어가는 썸네일에 xss 공격구문 삽입

<img width="782" alt="스크린샷 2020-02-06 오후 8 02 35" src="https://user-images.githubusercontent.com/54495632/73931732-252f7300-491c-11ea-8ded-23f18b64ae6f.png">





### 웹툰 댓글 작성


<img width="339" alt="스크린샷 2020-02-06 오후 8 00 56" src="https://user-images.githubusercontent.com/54495632/73931755-2eb8db00-491c-11ea-91d8-170e4313868c.png">


<img width="1565" alt="스크린샷 2020-02-06 오후 7 46 55" src="https://user-images.githubusercontent.com/54495632/73931763-31b3cb80-491c-11ea-905d-a9fd525cdd6a.png">





## NAVER BLOG




### 시도 목록

- 블로그 게시글
- 블로그 메모
- 블로그 메모 -> 카페 이동
- 블로그 안부
- 블로그 명
- 블로그 프로필



### 블로그 게시글

<img width="674" alt="스크린샷 2020-02-06 오후 8 52 38" src="https://user-images.githubusercontent.com/54495632/73934864-a7229a80-4922-11ea-897e-7cc58dc28efe.png">







### 블로그 메모

<img width="989" alt="스크린샷 2020-02-06 오후 8 32 31" src="https://user-images.githubusercontent.com/54495632/73933713-63c72c80-4920-11ea-9f7e-ab9b963e6b57.png">


### 블로그 메모 -> 카페 이동


<img width="843" alt="스크린샷 2020-02-06 오후 8 38 53" src="https://user-images.githubusercontent.com/54495632/73933867-b7397a80-4920-11ea-905e-d68be21ed630.png">


### 블로그 안부

<img width="992" alt="스크린샷 2020-02-06 오후 8 35 12" src="https://user-images.githubusercontent.com/54495632/73933731-6d509480-4920-11ea-9384-18fa822eace5.png">





### 블로그 명



<img width="349" alt="스크린샷 2020-02-06 오후 8 41 02" src="https://user-images.githubusercontent.com/54495632/73934022-01baf700-4921-11ea-8978-f9d6772a0780.png">





### 블로그 프로필



<img width="960" alt="스크린샷 2020-02-06 오후 8 47 06" src="https://user-images.githubusercontent.com/54495632/73934924-c4576900-4922-11ea-8a65-a462c620b047.png">







## NAVER Vibe



![스크린샷 2020-02-06 오후 9.13.48](/Users/shift_chill/Desktop/스크린샷 2020-02-06 오후 9.13.48.png)

```="" onMouseOver="alert('1')```  로 xss 구문 입력시 

" 는 &quot ; 으로 치환

'  는 &# 39; 로 치환 된다.