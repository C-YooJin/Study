## vue.js, angular, react 등 FE 관련 프레임워크
[FE 프레임워크 비교](https://kr.vuejs.org/v2/guide/comparison.html)

## Jquery, ajax
### Ajax (Asynchronous javascript and XML)
- 음, 지금은 XML만 사용하는 게 아니고 JSON등 다른 데이터 타입을 더 많이 사용함. 이름은 그렇지만.. 
- 비동기적으로 자바스크립트를 이용해서 서버와 통신할 수 있게 해주는 기술이다.
- 깜빡임 없이 화면을 넘기게 해 줌. url 변화도 없이.
- 사용자가 나중에 필요할 때 서버에서 가져오는 정보. 예를들어 메뉴바같은 것. 
- 이런 경우 서버 입장에서 데이터를 더 적게 사용할 수 있다는 장점이 있다
- 예제 코드1
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
- 예제 코드2
```
$.ajax({
    url: "/examples/media/request_ajax.php", // 클라이언트가 HTTP 요청을 보낼 서버의 URL 주소
    data: { name: "홍길동" },                          // HTTP 요청과 함께 서버로 보낼 데이터
    method: "GET",                                     // HTTP 요청 방식(GET, POST)
    dataType: "json"                                   // 서버에서 보내줄 데이터의 타입
})
// HTTP 요청이 성공하면 요청한 데이터가 done() 메소드로 전달됨.
.done(function(json) {
    $("<h1>").text(json.title).appendTo("body");
    $("<div class=\"content\">").html(json.html).appendTo("body");
})
// HTTP 요청이 실패하면 오류와 상태에 관한 정보가 fail() 메소드로 전달됨.
.fail(function(xhr, status, errorThrown) {
    $("#text").html("오류가 발생했습니다.<br>")
    .append("오류명: " + errorThrown + "<br>")
    .append("상태: " + status);
})
// HTTP 요청이 성공하거나 실패하는 것에 상관없이 언제나 always() 메소드가 실행됨.
.always(function(xhr, status) {
    $("#text").html("요청이 완료되었습니다!");
});
```
#### JSON.stringify() : json객체를 string 객체로 변환
- ajax의 data안에 사용한다
- 원본 `param -> {name:"yoojin", age: "1234"}`
- JSON.stringify() 적용 후 `param -> {"name":"yoojin", "age":"1234"}`
#### JSON.parse() : string객체를 json 객체로 변환
- success단에서 사용함
- `JSON.parse(param)`
- 결과 `{name:"yoojin", age: 1234}`

### const {a, b, c} = v;
[비구조화 할당](https://learnjs.vlpt.us/useful/06-destructuring.html)
```
const object = { a: 1, b: 2 };

const { a, b } = object;

console.log(a); // 1
console.log(b); // 2
```

### 동치연산자
- == (동등연산자)
  - 같은지 보는 거.. 만약 두 자료의 타입이 다르다면 타입 변환해서 검토해준다. 
- === (일치연산자)
  - 두 피연산자가 엄격하게 같은지 비교해준다. 타입까지 같아야 됨.

### 디자인 프레임워크
- [Bulma & tailwidn](https://medium.com/@im_37456/bulma-vs-tailwind-79da998c1d7a)
