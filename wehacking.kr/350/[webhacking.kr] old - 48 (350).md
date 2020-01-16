<img width="286" alt="스크린샷 2020-01-15 오후 3 34 20" src="https://user-images.githubusercontent.com/54495632/72411165-a6786780-37ad-11ea-9f02-2f5fc53687d7.png">



48번



<img width="409" alt="스크린샷 2020-01-15 오후 3 34 42" src="https://user-images.githubusercontent.com/54495632/72411186-b42ded00-37ad-11ea-8daa-53663cfc6b40.png">



파일 업로드 관련 문제인 것 같다.



<img width="343" alt="스크린샷 2020-01-15 오후 3 35 53" src="https://user-images.githubusercontent.com/54495632/72411203-be4feb80-37ad-11ea-94ec-e3349678c094.png">



소스코드도 딱히 별게 없고



<img width="756" alt="스크린샷 2020-01-15 오후 3 37 29" src="https://user-images.githubusercontent.com/54495632/72411211-c6a82680-37ad-11ea-8c77-08256c44e2ab.png">



파일 보내기 말고 윗칸에 아무거나 입력하여 엔터하니 다음과 같이 나왔다.

Delete도 가능하다.



<img width="336" alt="스크린샷 2020-01-15 오후 3 38 10" src="https://user-images.githubusercontent.com/54495632/72411256-e3dcf500-37ad-11ea-91a6-b1d7bc25d921.png">



delete 완료되고 나서 소스코드
?mode=del&time=1579070244

del과 time 으로 삭제가 결정된다.

Burp suite를 이용하니



<img width="440" alt="스크린샷 2020-01-15 오후 3 46 48" src="https://user-images.githubusercontent.com/54495632/72411777-13403180-37af-11ea-8eb3-f55e22756f29.png">



흠.. 딱히 특별한 건 없었다.

파일 업로드를 여러 번 시도하니 
memo + 업로드 파일이 있어야 업로드가 되는 것 같다.



<img width="375" alt="스크린샷 2020-01-15 오후 3 59 24" src="https://user-images.githubusercontent.com/54495632/72413193-90b97100-37b2-11ea-82dc-0e9e07f0856c.png">

다음과 같이 아무 파일이나 업로드 했다.

<img width="783" alt="스크린샷 2020-01-15 오후 4 00 45" src="https://user-images.githubusercontent.com/54495632/72413766-ddea1280-37b3-11ea-8b5e-c7254b5239c2.png">



파일 업로드 시 burp suite 에도 딱히 특별한 것이 없었고



<img width="790" alt="스크린샷 2020-01-15 오후 4 19 10" src="https://user-images.githubusercontent.com/54495632/72413280-cb230e00-37b2-11ea-9e7a-11fde37e4e41.png">





업로드가 되면 다음과 같이 칸이 생성된다.





<img width="272" alt="스크린샷 2020-01-15 오후 4 01 48" src="https://user-images.githubusercontent.com/54495632/72413300-dd04b100-37b2-11ea-99a9-5b6f147c3323.png">



업로드 시 URL



<img width="600" alt="스크린샷 2020-01-15 오후 4 19 48" src="https://user-images.githubusercontent.com/54495632/72413316-e2fa9200-37b2-11ea-956d-ff296af53871.png">





delete 시 URL

업로드 했을 때 URL을 보면 /upload/1.png 라고 나와 있는데 
upload라는 디렉토리 안에 업로드 했던 1.png파일이 존재하는 파일 시스템 구조로 되어있는 것 같다.

ls 명령어를 사용할 수 있으면 관련 디렉토리들을 모두 볼 수 있을 것 같았고 

delete시 파일을 지우니 rm + 파일명으로 실행되지 않을까 싶어서
rm과 동시에 ls를 실행하고자 파일 명을 &ls로 하고 업로드를 다시했다. -> rm&ls 실행





<img width="356" alt="스크린샷 2020-01-15 오후 3 54 26" src="https://user-images.githubusercontent.com/54495632/72413633-906da580-37b3-11ea-9ef7-722f933672b0.png">

<img width="930" alt="스크린샷 2020-01-15 오후 3 55 45" src="https://user-images.githubusercontent.com/54495632/72413623-8a77c480-37b3-11ea-9c66-bfdef1fa8086.png">



업로드 후 delete를 하니 ls가 실행되어 내부 파일들을 볼 수 있다.
FLAG 값이 나왔다.



<img width="448" alt="스크린샷 2020-01-15 오후 3 57 58" src="https://user-images.githubusercontent.com/54495632/72413653-9ebbc180-37b3-11ea-99fe-e41d184f6471.png">



해결.

delete시 rm으로 동작되므로 파일명을 ;ls로 해도 문제를 해결할 수 있다. ->rm;ls 가 실행