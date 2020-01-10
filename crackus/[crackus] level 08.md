<img width="152" alt="스크린샷 2020-01-10 오후 6 52 59" src="https://user-images.githubusercontent.com/54495632/72143686-8118e180-33da-11ea-81d2-6739b95593f2.png">

Lv8.

<img width="450" alt="스크린샷 2020-01-10 오후 6 53 05" src="https://user-images.githubusercontent.com/54495632/72143693-84ac6880-33da-11ea-954f-1222965743a1.png">

<img width="563" alt="스크린샷 2020-01-10 오후 6 53 10" src="https://user-images.githubusercontent.com/54495632/72143697-86762c00-33da-11ea-996e-dd5d0631e79b.png">

다음 문제의 쿼리를 보면 select id from play_sql08 where pw='' 이다.

딱히 id를 입력하는 칸이 없고 get 으로도 $pw 만 받게된다.

if(preg_match('/play|_|\.|\(|\)|info/i', $pw)){ exit("Nope !!");}
if(preg_match('/ /i', $pw)){ exit("Query is filtered :( ");}

preg_match 에 의해 공백이 필터링 되며 공백을 우회하는 방법은 많지만

이 문제에선 %0a 로 공백을 우회했다.

if($result[id] == "admin"){
    echo "C0n9raz!! Letz go 2 th3 n3xt L3v3l ^^";
    get_score();
  } 를 보면, 결국 result 가 admin 이여야 하므로

pw 에 true 값을 준 뒤 , UNION SELECT 를 이용하여 admin을 새로 넣어 주기로 했다.

pw=에 true를 입력하는 방법으로는 'or 1 , 0=0 등이 있지만 , 0=0 을 이용하였다.

WHERE 에 TRUE가 나올 수 있는 다른 조건을 이용해도 문제 해결이 가능하다.

<img width="494" alt="스크린샷 2020-01-10 오후 6 55 14" src="https://user-images.githubusercontent.com/54495632/72144174-71e66380-33db-11ea-98b6-ab52194530bc.png">

 공백이 필터링 되므로 pw=0=0'%0aUNION%0aSELECT%0a'admin

과 같이 URL을 입력해주었다.

<img width="748" alt="스크린샷 2020-01-10 오후 6 55 18" src="https://user-images.githubusercontent.com/54495632/72144236-92162280-33db-11ea-93b0-d7c319ec67ee.png">

전체 쿼리문을 보게되면 다음과 같다.