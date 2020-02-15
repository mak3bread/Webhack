# NAVER BugBounty



## Series NAVER

e북 관련해서 리뷰 댓글에 XSS를 시도했다.

<img width="801" alt="스크린샷 2020-02-15 오후 8 01 50" src="https://user-images.githubusercontent.com/54495632/74586826-d1650e00-502e-11ea-9bf3-18026d6244f8.png">


<img width="801" alt="스크린샷 2020-02-15 오후 8 03 03" src="https://user-images.githubusercontent.com/54495632/74586828-d924b280-502e-11ea-91ba-9aa23bddff40.png">

<img width="800" alt="스크린샷 2020-02-15 오후 8 05 21" src="https://user-images.githubusercontent.com/54495632/74586831-dd50d000-502e-11ea-9b21-7eefc4804925.png">


태그 꺽쇠 < 가 존재하면 자동으로 > 닫는 꺽쇠가 생성되어 필터링 된다고 생각했는데
/에 의해 나눠지는 곳이 결정되는 것 같다.
<script>alert(1);</script> 는 그대로 입력이 가능
<img width="855" alt="스크린샷 2020-02-15 오후 8 09 59" src="https://user-images.githubusercontent.com/54495632/74586875-67993400-502f-11ea-85bd-3d67dd364bde.png">

<img width="846" alt="스크린샷 2020-02-15 오후 8 10 24" src="https://user-images.githubusercontent.com/54495632/74586877-6d8f1500-502f-11ea-8079-bead4a8c9c68.png">


<img width="727" alt="스크린샷 2020-02-15 오후 8 10 54" src="https://user-images.githubusercontent.com/54495632/74586878-78e24080-502f-11ea-8ed1-4aa9b026cbbd.png">

XSS가 바로 가능한 구조는 아닌듯 싶다.






## NAVER Cafe





### 사진 SNS 연동

카페에 있는 기능이였지만 nid.naver.com 에 reflected xss 를 시도했다고 볼 수 있다.

<img width="728" alt="스크린샷 2020-02-15 오후 9 00 09" src="https://user-images.githubusercontent.com/54495632/74587487-5273d380-5036-11ea-965c-a2b20de82e62.png">


nid.naver.com 에서 필터링 되는 조건이
< 꺽쇠괄호 -> &lt; 으로 필터링 되고
&lt; 에서 & 기호가 &amp; 로 필터링 된다.

```<img src=`` onerror=this.onerror=confirm(1) ```

원래 공격한 구문이 이거 였으니
= , ` ( ) . 등은 필터링이 안되므로

&나 < > 가 없는 공격 방법을 찾아봐야겠다.





### 카페 연혁

<img width="872" alt="스크린샷 2020-02-15 오후 9 34 52" src="https://user-images.githubusercontent.com/54495632/74587862-0d05d500-503b-11ea-8835-674a6a55bf56.png">

다음과 같은 카페 연혁에  파일 업로드를 시도해봤다.

<img width="138" alt="스크린샷 2020-02-15 오후 9 34 38" src="https://user-images.githubusercontent.com/54495632/74587864-12fbb600-503b-11ea-8f74-0caa59a15376.png">

다음과 같은 파일을 업로드 하면

<img width="1424" alt="스크린샷 2020-02-15 오후 9 34 23" src="https://user-images.githubusercontent.com/54495632/74587867-2d359400-503b-11ea-8816-cefe5bdf4cac.png">

업로드 할 때 부터 필터링이 되지 않지만 서버에 올라가고 해당 파일 이름이 어떤 암호화 과정을 거쳐 다시 업로드 되는 것 같다.

해당 URL 에서 reflected XSS도 시도해봤지만 



<img width="711" alt="스크린샷 2020-02-15 오후 9 29 02" src="https://user-images.githubusercontent.com/54495632/74587886-59511500-503b-11ea-83f3-a78e213c0597.png">

? 중국인 개발자가 있나 

<img width="431" alt="스크린샷 2020-02-15 오후 9 40 46" src="https://user-images.githubusercontent.com/54495632/74587956-e1371f00-503b-11ea-911d-917c410bc667.png">

<img width="381" alt="스크린샷 2020-02-15 오후 9 40 32" src="https://user-images.githubusercontent.com/54495632/74587958-e2684c00-503b-11ea-902d-bd1320c8a0bf.png">


다시 보니 파일명 자체도 필터링이 된다 . < > 꺽쇠 필터링

<img width="506" alt="스크린샷 2020-02-15 오후 9 41 54" src="https://user-images.githubusercontent.com/54495632/74587974-0035b100-503c-11ea-8ad2-b6c80aa89bd9.png">

&도 필터링 ..

<img width="501" alt="스크린샷 2020-02-15 오후 9 45 02" src="https://user-images.githubusercontent.com/54495632/74588021-79350880-503c-11ea-9f28-ad2bed1d3709.png">

\ 필터링.. 다 막아뒀다.