## Naver Bug Bounty Program

https://bugbounty.naver.com/ko/ 를 복사하여 작성했습니다

- ### 1. 소개

  네이버 버그 바운티 프로그램은 네이버 서비스의 취약점을 조기에 찾아 사용자들에게 안전한 서비스를 제공하기 위한 프로그램입니다. 전 세계의 보안 전문가들의 도움으로 네이버 서비스의 보안 취약점을 빠르게 찾아 고치고, 보안 전문가들의 노력에 적절한 포상을 지급함으로써 네이버 서비스를 더욱 안전하게 만드는 일을 장려합니다.

- ### 2. 범위

  하단의 웹사이트에서 발생하는 취약점들을 대상으로 합니다.

  - 네이버 페이 : pay.naver.com 및 *.pay.naver.com
  - 네이버 블로그 : blog.naver.com 및 *.blog.naver.com
  - 네이버 카페 : cafe.naver.com 및 *.cafe.naver.com
  - 네이버 영화 : movie.naver.com, 및 *.movie.naver.com. 단, ticket.movie.naver.com은 제외
  - 네이버 쇼핑 : shopping.naver.com 및 *.shopping.naver.com
  - 네이버 바이브 : vibe.naver.com 및 *.vibe.naver.com
  - 네이버 웹툰 : comic.naver.com 및 *.comic.naver.com
  - 네이버 시리즈 : series.naver.com 및 *.series.naver.com
  - 네이버 예약 : booking.naver.com 및 *.booking.naver.com
  - 네이버 파파고 : papago.naver.com 및 *.papago.naver.com
  - 네이버 회원 : nid.naver.com 및 *.nid.naver.com
  - 그리고 위 서비스에서 사용하는 API Gateway(apis.naver.com)도 포함합니다.

  하단의 최신버전 어플리케이션에서 발생하는 취약점들을 대상으로 합니다. 

  - 네이버 툴바
  - 네이버 백신
  - 클라우드 탐색기

- ### 3. 포상

  |                 취약점                 |                             예시                             |   포상금액   |
  | :------------------------------------: | :----------------------------------------------------------: | :----------: |
  |            Account takeover            |                    Authentication Bypass                     | USD $1,000 ~ |
  |         Remote Code Execution          | Ability to send packets containing arbitrary system call to the client or server side | USD $1,000 ~ |
  | Full access to file system or database |                        SQL Injection                         | USD $1,000 ~ |
  |       Execute code on the client       |                             XSS                              |  USD $200 ~  |
  |           Logical flaw Bugs            |          Sensitive actions by user, Purchase Bypass          |  USD $200 ~  |
  |  Other valid security vulnerabilities  |                  Information Leakage, CSRF                   |  USD $100 ~  |

  - CSRF 취약점은 다음의 기능만 대상으로 합니다 : 네이버 회원 정보, 네이버 카페 관리, 네이버 블로그 관리
  - 포상금은 취약점의 위험도와 보고서 등을 종합적으로 검토하여 주어집니다.
  - 사용자의 개입이 많이 필요한 경우 포상 금액이 줄어들 수 있습니다.
  - 새로운 방식의 공격 기법이나 버그타입에 대해서는 좀 더 많은 포상금이 주어질 수 있습니다.

- ### 4. 포상 대상에서 제외되는 경우

  다음과 같은 경우들은 포상 대상에서 제외됩니다.

  - 버그 리포트를 받았을 시점에서 취약점이 재현되지 않는 경우
  - 버그 리포트를 받았을 시점에서 취약점이 재현되더라도 네이버 내부에서 취약점에 대한 인지를 하고 있을 경우
    -  예를 들면 1 Day 취약점으로 인해 네이버 서비스가 미처 수정되지 못하였을 때,
    -  이 경우는 네이버 보안팀에서 보고자에게 내부에서 발견된 경위, 시점에 대해서 충분한 설명을 합니다.
  - 취약점 증명 이외에 불필요한 행위를 통해 서버의 정보를 획득한 경우
  - 다른 사람이 먼저 제보한 취약점
  - 이미 공개적으로 알려진 취약점
  - 증명 없이 가능성만을 제시한 경우
  - Denial-of-Service(DoS) 공격
  - 너무 많은 사용자의 개입이 필요한 경우
  - 보안 기능을 끄고 취약점을 발생 시킨 경우
  - 이미 다른 곳에 제보한 취약점(KISA 외)
  - naver.net 에서의 XSS
  - URL Redirection
  - Clickjacking
  - 에러페이지를 이용한 페이지 변조
  - Security, CSP 헤더 관련
  - 서비스의 특정 기능의 Replay
  - 본인에게만 영향이 미치는 취약점(Self XSS)
  - 서버의 어플리케이션 정보 노출
  - SSL 미적용으로 인한 쿠키 탈취
  - 그 외 보안상 위협이 없다고 판단되는 취약점

- ### 5. 제한 사항 및 공개 정책

  제한 사항 및 공개 정책입니다.

  - 취약점이 고쳐지고 대부분의 사용자가 업데이트를 할때까지 취약점에 대한 자세한 정보는 공개하지 말아주시기 바랍니다. 단, 네이버 보안팀에게 허가되는 경우는 취약점에 대해서 공개할 수 있습니다.
  - 다른 사용자에게 피해를 끼칠 수 있는 행위는 삼가주시기 바랍니다.
  - 네이버 및 계열사 임직원 은 해당 프로그램에 참여할 수 없습니다.

- ### 6. 제보

  취약점은 [이곳](https://bugbounty.naver.com/servicedesk/customer/portal/3)을 통해 제보해주시기 바랍니다. 보고서에는 다음과 같은 사항들을 포함하면 좋습니다.

  - 취약점 이름
  - 취약점의 발견 방법
  - 버그를 재현하기 위한 코드
  - 발생한 서비스 및 도메인
  - 해당 취약점이 보안상 어떤 위협이 될 수 있는지에 대한 설명

- 기타 문의 사항은 [dl_naverbugbounty@navercorp.com](mailto:dl_naverbugbounty@navercorp.com)으로 보내주시기 바랍니다.

  ※ 절대 취약점은 이메일에 작성하지 마시기 바랍니다.