![img](https://k.kakaocdn.net/dn/DrrCt/btqAUvD39s1/4NdeHSs5rDzkDhTuyOAUG1/img.png)



250 첫 문제

 



![img](https://k.kakaocdn.net/dn/bE8fhQ/btqAQNfonh6/KblcLHfnY7yayOzRafByQk/img.png)



첫 화면을 보면 다음과 같다.

O 인 점? 노란색 선 GOAL 까지 옮기게 되면 solve가 가능한듯 싶다.

 



![img](https://k.kakaocdn.net/dn/c4qdfj/btqAU6YlTSl/HprQcerklouav4jkkPcDt0/img.png)



 

소스코드를 보니 왼쪽으로 1600px 인 위치에 도달하게 되면

 

this.href='?go='+this.style.left 로 이동되어 해결될 것 같다.

 

현재 소스코드의 상태에선 O 를 한 번 클릭하면 1px 만큼 조금 씩 이동하게 된다.

 



![img](https://k.kakaocdn.net/dn/b4oR7c/btqASzfVW27/OJPA9K2opry5S6k0OqF201/img.png)



첫 화면과 다르게 O 를 누르니 조금 씩 이동이 되는 것을 확인 할 수 있다.

 

 



![img](https://k.kakaocdn.net/dn/bVQ5Hn/btqASyuw0vn/w1zz3aBTsUa85Esghd1a40/img.png)



다시 소스 코드로 돌아와서 한 번 (on click) 마다 1px 증가하는 것을 400px 씩 움직이도록 지정하고

 

1600px 가 넘어가면 if 문이 실행되도록 설정해보았다.

 



![img](https://k.kakaocdn.net/dn/ZuN7Q/btqARyof6GE/xSpvJfoWC5PiHtXwfhBmK0/img.png)



이러한 소스코드 수정 후 O를 클릭하니

 

no hack 와 함께 해당 명령이 거절 당했다.

 

 



![img](https://k.kakaocdn.net/dn/bVo5K0/btqAU5E9cgc/mY2gVceZIuPCD7AkMzcN01/img.png)



 

Chrome 에서 진행이 안되고

 

internet exploer 에서 위와 같이 진행하게 되면 해결이 가능하다.