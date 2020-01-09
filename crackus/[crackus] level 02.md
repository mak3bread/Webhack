<img width="167" alt="스크린샷 2020-01-09 오후 6 31 06" src="https://user-images.githubusercontent.com/54495632/72057366-a2fa6180-3311-11ea-9906-9c3891ca9a4f.png">


crackus Lv2. 

<img width="844" alt="스크린샷 2020-01-09 오후 6 51 07" src="https://user-images.githubusercontent.com/54495632/72057372-a55cbb80-3311-11ea-9531-3cf69490094c.png">


if($result['id'] == 'admin'){
    echo "C0n9raz!! Letz go 2 th3 n3xt L3v3l ^^";
    get_score();
  }

이 부분을 보면 id가 admin 인 경우 다음레벨로 넘어갈 수 있는 것 같다.

쿼리 문이 $query = "SELECT id FROM play_sql02 WHERE id='$id' and pw=sha1('$pw')";

와 같이 나와있었는데 sha1 으로 암호화 되어 있었다.

id 에 admin 을 넣어주고 그 뒤에 pw는 주석 처리를 하는 쿼리문을 생각했다.

SELECT id FROM play_sql01 WHERE id='admin'# 와 같으면 주석 처리 이후

쿼리문이 어떻게 와도 관계 없이 TRUE 처리 된다.

다음과 같이 URL 을 넣어 처리했다.

<img width="483" alt="스크린샷 2020-01-09 오후 6 36 23" src="https://user-images.githubusercontent.com/54495632/72057391-ad1c6000-3311-11ea-8229-8442bbcf0ea4.png">

굳이 id 가 admin 이 아니여도 다음과 같은 형태로도 해결이 가능하다.

<img width="682" alt="스크린샷 2020-01-09 오후 7 04 59" src="https://user-images.githubusercontent.com/54495632/72058211-0933b400-3313-11ea-8eb5-2b296f972782.png">
