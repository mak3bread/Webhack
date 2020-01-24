<img width="268" alt="스크린샷 2020-01-24 오후 6 01 58" src="https://user-images.githubusercontent.com/54495632/73069730-d59b8100-3ef1-11ea-8eb9-c924eb765b27.png">

17번

<img width="795" alt="스크린샷 2020-01-24 오후 6 02 11" src="https://user-images.githubusercontent.com/54495632/73069940-670af300-3ef2-11ea-94b4-7ec5f43a3186.png">

$_GET['id'] = strrev(addslashes($_GET['id']));
$_GET['pw'] = strrev(addslashes($_GET['pw']));

id , pw 각각 strrev 함수와 addslashes 함수가 붙었다.

addslashes 함수는 이전 문제에서도 나온 적이 있는데 
' " \ 즉 작은 따옴표, 큰 따옴표 백슬래시가 오는 경우 \ 를 하나 더 추가해주는 함수이다.

strrev 함수는 매개변수로 오게되는 문자열을 거꾸로 출력해주는 함수 이다.
예를 들어, id=strrev(admin); 으로 입력되면, id에는 admin을 거꾸로 한 nimda가 입력된다.

두 함수를 이용하여 URL GET을 이용해 ?id=" 와 같이 입력하게 되면
$_GET['id']=strrev(addslashes(")); 와 같다.
$_GET['id']=strrev(\"); 이 되고 결국
id에 "\ 가 입력되어 전체 쿼리로 보면

id='"\' and pw='' 와 같은 꼴이 될 것이다. 이 때 id 값으로 "\' and pw = 가 입력된다.
' 작은 따옴표 하나가 남고 id=false 이므로 뒤에 id =false || 1# 과 같은 쿼리를 생각했다. 

따옴표나 \ 백슬래쉬를 이용하지 않으므로 strrev 함수만 고려하여 반대로 입력하면
?id="&pw=%231|| 과 같이 URL을 입력하면,
id='"\' and pw='||1#' 과 같은 쿼리가 되며 해당 where절이 TRUE가 되서
문제가 해결이 된다.

<img width="824" alt="스크린샷 2020-01-24 오후 10 23 30" src="https://user-images.githubusercontent.com/54495632/73073310-74c47680-3efa-11ea-98cb-31e68724b6b8.png">
