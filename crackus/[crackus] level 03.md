<img width="172" alt="스크린샷 2020-01-09 오후 7 14 21" src="https://user-images.githubusercontent.com/54495632/72059697-db9c3a00-3315-11ea-9a37-601f91696fac.png">

Lv 3. 시작

<img width="559" alt="스크린샷 2020-01-09 오후 7 26 19" src="https://user-images.githubusercontent.com/54495632/72059782-05556100-3316-11ea-9e27-ee28b0803548.png">

and 와 or 에 대해 필터링 조건이 있어
or 대신 || 를 사용해도 되지만 출제의도가 그건 아닌 것 같아 
다른 쿼리문을 생각했다.

SELECT ID FROM play_sql03 where id =' '=false#(주석처리)
같이 표현하면 해결이 가능하다.

<img width="688" alt="스크린샷 2020-01-09 오후 7 20 09" src="https://user-images.githubusercontent.com/54495632/72059891-3cc40d80-3316-11ea-80b4-0ccc0c67879b.png">

<img width="631" alt="스크린샷 2020-01-09 오후 7 20 23" src="https://user-images.githubusercontent.com/54495632/72059898-3fbefe00-3316-11ea-8a50-0abc952f4278.png">

<img width="683" alt="스크린샷 2020-01-09 오후 7 29 43" src="https://user-images.githubusercontent.com/54495632/72059972-68df8e80-3316-11ea-8ebc-79485e7b2afb.png">

다음과 같은 3 가지 false SQL Injection 방법으로 
공백 = 공백 -> true
false =false -> true 
문제를 해결 할 수 있다. 
#는 %23 로 URL 인코딩된 값을 전달해준다.

굳이 or 을 사용하고 싶다면

<img width="728" alt="스크린샷 2020-01-09 오후 7 16 49" src="https://user-images.githubusercontent.com/54495632/72060079-a7754900-3316-11ea-9683-8b31a3ed2a31.png">

와 같이 해결할 수 있다. or 과는 다르게 || 는 || 이후 문자에 대해 띄어쓰기가 필요하지 않다.
