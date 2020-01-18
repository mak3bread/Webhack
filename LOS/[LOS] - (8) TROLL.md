<img width="178" alt="스크린샷 2020-01-16 오후 7 49 59" src="https://user-images.githubusercontent.com/54495632/72520635-2fba9780-389d-11ea-8bf5-9d091e87f882.png">

8번 트롤

<img width="507" alt="스크린샷 2020-01-16 오후 7 50 22" src="https://user-images.githubusercontent.com/54495632/72520647-36e1a580-389d-11ea-8975-3bcf2fc5f45f.png">

간단한 문제이다.

preg_match 함수를 찾아보면 된다.

소스코드를 보면,
if(preg_match('/\'/i', $_GET[id])) exit("No Hack ~_~");
if(preg_match("/admin/", $_GET[id])) exit("HeHe");

' 따옴표와 admin을 필터링하는데
admin preg_match 함수엔 끝 부분에 i 가 없다.
i가 붙는 경우 대소문자를 구분한다는 의미고 i 가 붙지 않을 경우 대소문자를 구분하지 않는다.

id = ADMIN 만 하면 되는 문제이다.

<img width="696" alt="스크린샷 2020-01-16 오후 8 27 19" src="https://user-images.githubusercontent.com/54495632/72521386-a6a46000-389e-11ea-9723-fcb651048437.png">
