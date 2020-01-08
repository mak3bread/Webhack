![img](https://k.kakaocdn.net/dn/Tb8qc/btqAVHcYozK/3knmg3kkVwUXt2QdPpQwik/img.png)



12번

 



![img](https://k.kakaocdn.net/dn/3akXf/btqARXg4rZ9/oQu2W2VL4ZFoTk6P79wbSk/img.png)



JAVA script 와 관련된 문제인것 같다.

 



![img](https://k.kakaocdn.net/dn/9Zvpl/btqASynL9eI/Y0kLBZrV3kKek5HKxNxD7k/img.png)



?! 다음과 같은 이모티콘들이 등장하였다.

 

console 창으로 이동 하여 돌려보기로 하였다.

 



![img](https://k.kakaocdn.net/dn/2jy4d/btqAQNzFVM6/6FTR6ZaQ5vWneeKYcChB6K/img.png)



 

전체를 복사 하고 콘솔창에 붙여 넣기 하니  마지막 부분에 ; 가 있었고 실행 시켜보았으나

 

해당 관련 코드가 없는지 undefined 만 출력됐다.

 

콘솔 창에 복사 된 마지막 부분 코드와 전체적으로 보니 

 

js 코드 특징 상 이모티콘? 이 이어지는 부분을 + 로 표현한 것 같았고

 

마지막 부분  쪽에 이미 괄호로 닫혔는데 + 없이 ('_'); 가 혼자 동떨어져 있어

 

해당 부분을 지우고 마지막 부분에  ; 를 넣었다.

 

 



![img](https://k.kakaocdn.net/dn/A5WSs/btqAVHYlDXG/qicyKFnKPOU59HrNgfwOs0/img.png)



 

실행시키니 다음과 같은 함수가 나왔고 클릭을 했다. 

 



![img](https://k.kakaocdn.net/dn/burGxS/btqAUvD4X3K/eGdsKtrnzdF9KUJNdTjFYk/img.png)



 

화면은 중간에 짤려 전체 함수를 가지고 왔다.

 

(function anonymous() 

{
var enco='';
var enco2=126;
var enco3=33;
var [ck=document.URL.substr(document.URL.indexOf('='));](https://while-0.tistory.com/ck=document.URL.substr(document.URL.indexOf('='));)
for(i=1;i<122;i++){
 enco=enco+String.fromCharCode(i,0);
}
function enco_(x){
 return enco.charCodeAt(x);
}
if(ck=="="+String.fromCharCode(enco_(240))+String.fromCharCode(enco_(220))+String.fromCharCode(enco_(232))+String.fromCharCode(enco_(192))+String.fromCharCode(enco_(226))+String.fromCharCode(enco_(200))+String.fromCharCode(enco_(204))+String.fromCharCode(enco_(222-2))+String.fromCharCode(enco_(198))+"~~~~~~"+String.fromCharCode(enco2)+String.fromCharCode(enco3)){
 [location.href=](https://while-0.tistory.com/location.href=)"./"+ck.replace("=","")+".php";
 }
 }

)

 

ck 변수는 URL의 '=' 문자의 index 주소 부터 (위치) 짤라서 저장한다.

 

for 문과 function enco_(x) 에 의해 각 enco_ 에 할당이 된다.

 

if 문을 만족하게 되면 해결이 되는 것 같아

 

해당 ck 를 만족시킬 문자열을 찾기로 했다.

 



![img](https://k.kakaocdn.net/dn/QdQnG/btqARjkzqTE/lDMSMTlkktTFauGSxkaJYK/img.png)



다음과 같이 해당 함수에서 함수 선언 부분과 if 조건 부분 , if 조건 만족했을 때 실행 부분을 제거하여

 

youaregod~~~~~~~! 이 출력됨을 확인 했다.

 



![img](https://k.kakaocdn.net/dn/bBvJBD/btqAUuyqAJr/IXbNXRKEgGfWq9zLbEvzO0/img.png)



 

입력 자체는 ?=youaregod~~~~~~~!



![img](https://k.kakaocdn.net/dn/brHHE0/btqATgHarXI/YJ8tFnqMfkV7PeaDlgGS3k/img.png)



와 같이 해주어야 된다.