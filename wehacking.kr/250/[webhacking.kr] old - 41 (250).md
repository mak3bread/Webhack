<img width="276" alt="스크린샷 2020-01-06 오후 11 29 18" src="https://user-images.githubusercontent.com/54495632/71824238-67c31d00-30dc-11ea-824d-52cb4b7c3540.png">

41 번 !

<img width="385" alt="스크린샷 2020-01-06 오후 11 29 52" src="https://user-images.githubusercontent.com/54495632/71824277-83c6be80-30dc-11ea-950b-e44dcc56a705.png">

첫 화면이다. 파일 업로드 관련 문제인 것 같다.

<img width="720" alt="스크린샷 2020-01-06 오후 11 30 01" src="https://user-images.githubusercontent.com/54495632/71824291-8de8bd00-30dc-11ea-983b-dde4a7c868e5.png">

제출을 누르니 아무것도 없는 상태로는 제출이 안된다.

view-source 로 소스코드를 확인했다.

<img width="515" alt="스크린샷 2020-01-06 오후 11 30 14" src="https://user-images.githubusercontent.com/54495632/71824443-de601a80-30dc-11ea-8030-c68f8439e7b7.png">

isset 함수는 변수가 존재하면 , true 아니면 false를 리턴한다. 

그래서 이전 화면에서 아무것도 없이 제출을 했을 때 오류 메세지가 출력된 듯 싶다.

name은 제출한 원래 파일의 이름에서 . < > / 등이 필터링 된 후 $fn 에 저장된다.

$cp 에는 tmp_name 이 저장 된다.

copy 함수는 copy("a","b"); 구조라고 가정했을 때 

a 는 기존 파일을 의미하고 b는 옮길 곳과 이름을 의미한다.

$upload_dir 위치에 필터링된 $fn이름으로 저장되는 것 같다.

경로 ./$upload_dir/$fn 에 저장된 파일에 $flag 가 있다.

<img width="907" alt="스크린샷 2020-01-07 오전 12 58 35" src="https://user-images.githubusercontent.com/54495632/71888464-921be580-3183-11ea-964e-eabf45d0066a.png">

필터링 되는 아무것도 없는 파일로 업로드를 시도하면 다음과 같은 오류 메세지가 출력된다.

index.php 의 경로가 출력된다. 아무 것도 이름이 없는 상태에서는 원하는 경로를 얻을 수 없었고

파일의 최대 길이를 초과하는 copy 함수 오류를 이용했다.

<img width="392" alt="스크린샷 2020-01-07 오후 9 09 11" src="https://user-images.githubusercontent.com/54495632/71894584-0067a480-3192-11ea-8ef6-7b107882dbae.png">


<img width="919" alt="스크린샷 2020-01-07 오후 9 06 12" src="https://user-images.githubusercontent.com/54495632/71894519-d7dfaa80-3191-11ea-8229-3fd70e31adf0.png">

<img width="127" alt="스크린샷 2020-01-07 오후 9 08 55" src="https://user-images.githubusercontent.com/54495632/71894568-f8a80000-3191-11ea-8391-31407cd8666e.png">

다음과 같이 파일명이 엄청 긴 파일을 업로드 하여 파일이 저장된 경로를 얻을 수 있었고

아무것도 없는 임의의 파일을 업로드 하고 해당 경로 + 파일 이름으로 접근하였다.

<img width="136" alt="스크린샷 2020-01-07 오후 9 09 58" src="https://user-images.githubusercontent.com/54495632/71894642-3442ca00-3192-11ea-8a92-45cbfe617c23.png">

<img width="452" alt="스크린샷 2020-01-07 오후 9 10 31" src="https://user-images.githubusercontent.com/54495632/71894648-373dba80-3192-11ea-8f4c-ed2963bd29cd.png">

<img width="625" alt="스크린샷 2020-01-07 오후 9 06 38" src="https://user-images.githubusercontent.com/54495632/71894671-4290e600-3192-11ea-964e-83dbe3c4f28e.png">

<img width="705" alt="스크린샷 2020-01-07 오후 8 18 45" src="https://user-images.githubusercontent.com/54495632/71894686-4b81b780-3192-11ea-9eff-2dfc76a34568.png">

그 결과 FLAG 값을 받을 수 있었고

<img width="409" alt="스크린샷 2020-01-07 오후 8 19 18" src="https://user-images.githubusercontent.com/54495632/71894708-5a686a00-3192-11ea-8095-ac86049ca02e.png">

auth 에 해당 FLAG를 입력하여 문제를 해결하였다.
