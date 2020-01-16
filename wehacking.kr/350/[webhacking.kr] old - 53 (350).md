<img width="287" alt="스크린샷 2020-01-16 오후 5 22 18" src="https://user-images.githubusercontent.com/54495632/72506271-ed855c00-3884-11ea-98a5-964a653844d1.png">

53번

<img width="415" alt="스크린샷 2020-01-16 오후 5 22 21" src="https://user-images.githubusercontent.com/54495632/72506280-f1b17980-3884-11ea-8db2-6405808e17a3.png">

딱히 별게 없다 . view-source

<img width="828" alt="스크린샷 2020-01-16 오후 5 22 26" src="https://user-images.githubusercontent.com/54495632/72506302-f7a75a80-3884-11ea-8471-c71b97c85afa.png">

if(preg_match("/select|by/i",$_GET['val'])) exit("no hack");
preg_match 함수에 의해 get으로 받은 val값 중 select나 by를 필터링 한다.

$result = mysqli_fetch_array(mysqli_query($db,"select a from $hidden_table where a={$_GET['val']}"));
hidden_table에서 a=val 인 a 를 가져온다.

테이블 명 자체는 숨겨져 있고 해당 테이블 명이 answer로 보낸 값과 같으면 해결된다. union select를 이용하고자 했으나 select가 막혀 있었다.

UNION select 없이 테이블 명을 찾는 방법을 검색해서
procedure analyse() 를 찾았다.

쿼리문 where 절을 true 로 만들고 뒤에 procedure analyse() 를 붙이면
해당 정보를 알 수 있는듯 하다.

URL은 val=a procedure analyse() 와 같이 주었다.

<img width="607" alt="스크린샷 2020-01-16 오후 5 35 08" src="https://user-images.githubusercontent.com/54495632/72507341-0e4eb100-3887-11ea-8f3a-49b52c38a124.png">

webhacking.chall53_755fdeb36d873dfdeb2b34487d50a805.a 
와 같이 값이 나오게 되는데 
db.table_name.column 의 형식으로 출력되므로
table_name 가운데 부분인 chall53_755fdeb36d873dfdeb2b34487d50a805 만 필요하다.

<img width="613" alt="스크린샷 2020-01-16 오후 5 38 04" src="https://user-images.githubusercontent.com/54495632/72507522-62f22c00-3887-11ea-9b6a-e28c61bfc572.png">