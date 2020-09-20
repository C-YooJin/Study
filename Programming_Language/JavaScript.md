## vue.js, angular, react 등 FE 관련 프레임워크
[FE 프레임워크 비교](https://kr.vuejs.org/v2/guide/comparison.html)

## Jquery, ajax
### Ajax (Asynchronous javascript and XML)
- 음, 지금은 XML만 사용하는 게 아니고 JSON등 다른 데이터 타입을 더 많이 사용함. 이름은 그렇지만.. 
- 비동기적으로 자바스크립트를 이용해서 서버와 통신할 수 있게 해주는 기술이다.
- 깜빡임 없이 화면을 넘기게 해 줌. url 변화도 없이.
- 사용자가 나중에 필요할 때 서버에서 가져오는 정보. 예를들어 메뉴바같은 것. 
- 이런 경우 서버 입장에서 데이터를 더 적게 사용할 수 있다는 장점이 있다
- 예제 코드
```
$.ajax({
	type: "GET", //요청 메소드 방식
	url:"/AjaxTest/ex01.do",
	dataType:"text", //서버가 요청 URL을 통해서 응답하는 내용의 타입
	success : function(result){
		//서버의 응답데이터가 클라이언트에게 도착하면 자동으로 실행되는함수(콜백)
		//result - 응답데이터
		//$('#result').text(result);
		alert(result);
	},
	error : function(a, b, c){
		//통신 실패시 발생하는 함수(콜백)
		alert(a + b + c);
	}
});
```
