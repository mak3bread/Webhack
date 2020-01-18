<img width="287" alt="스크린샷 2020-01-13 오후 3 03 01" src="https://user-images.githubusercontent.com/54495632/72235596-6763de00-3616-11ea-86e1-72ecce384526.png">

60번 마지막 300

<img width="388" alt="스크린샷 2020-01-13 오후 3 03 16" src="https://user-images.githubusercontent.com/54495632/72235604-6d59bf00-3616-11ea-9429-0ebcacb398b3.png">

idx.. index? 값이 나오고 접근이 거부됐다고 한다.

<img width="788" alt="스크린샷 2020-01-13 오후 3 03 28" src="https://user-images.githubusercontent.com/54495632/72235612-7cd90800-3616-11ea-9675-de680adf5dcf.png">

if(!is_numeric($_COOKIE['PHPSESSID'])) exit("Access Denied<br><a href=./?view_source=1>view-source</a>");
쿠키의 PHPSESSID에 숫자가 아닌 값이 있으면 접근이 거부 된다.

if($_GET['mode']=="auth"){
mode =auth를 주기로 했다.

다음 두 조건을 맞추면,

<img width="570" alt="스크린샷 2020-01-13 오후 3 06 07" src="https://user-images.githubusercontent.com/54495632/72235647-a7c35c00-3616-11ea-91cc-d553b33ae130.png">

다음과 같이 접근이 가능해지게 된다.

 $p = fopen("./readme/{$_SESSION['idx']}.txt","w");
  fwrite($p,$_SESSION['idx']);
  fclose($p);
  if($_SERVER['REMOTE_ADDR']!="127.0.0.1"){
    sleep(1);
    unlink("./readme/{$_SESSION['idx']}.txt");
  }

readme.txt에 flag가 있을 것 같다.
여기서 ip주소가 127.0.0.1이 아니면 1초간 sleep 후 파일을 언링크 한다.
하지만 , auth 에 접근하기 전 sleep 1초가 진행된다.

하나의 세션으로 접근함과 동시에
삭제가 되기 전 1초 안에 다른 세션으로 접근하여 해결을 했다.

페러럴즈를 이용해서 윈도우 환경으로 다른 세션값과 쿠키 값을 준 뒤
Mac OS 로 해당 사이트에 동시 접근 하여 해결이 됐다.


<img width="451" alt="스크린샷 2020-01-13 오후 3 49 32" src="https://user-images.githubusercontent.com/54495632/72237213-0986c480-361d-11ea-9378-ece048a3900f.png">

<img width="441" alt="스크린샷 2020-01-13 오후 3 49 39" src="https://user-images.githubusercontent.com/54495632/72237214-0d1a4b80-361d-11ea-9b12-eb7116cabdf7.png">