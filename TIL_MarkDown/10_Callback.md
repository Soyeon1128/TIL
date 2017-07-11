# 콜백 함수

> 어떠한 정보(또는 이벤트)를 관리하는 대상이 자신의 정보가 변경되거나 또는 이벤트가 발생할때 자신의 변경된 정보나 이벤트에 따른 어떠한 처리를 할 수 있도록 제공하는 함수

- 객체의 상태 변화(이벤트)가 발생 하였을 경우, 이러한 사실을 콜백함수를 통해 전달한다.
- 특정 함수의 동작이 끝남과 동시에, 다른 여러 가지 함수를 호출해야 할 경우에 사용된다.
- 키보드나 마우스 클릭과 같은 디바이스 이벤트 뿐만이 아니라 Ajax, 데이터 처리 등 많은 부분에서 사용되고 있다.

### * 시계의 알람 기능과 유사

```javascript
function alram(min, callback) {
     var isCall = false;
     setInterval(function() {
          var date = new Date();
          var nowMin = date.getMinutes();

          if(nowMin == min && !isCall) {
               isCall = true;
               callback(nowMin);
          }
     }, 1000);
}

onload=function() {
     alram(15, function(min) {
          alert("현재 Minutes는'" + min + "' 입니다.");
     });
}
```

### * AJAX 비동기 통신과 콜백함수를 사용하는 이유
 : 비동기 통신은 특정 기능을 요청하고 다른 작업을 하고 있다가 요청한 처리가 끝난 후, 콜백함수가 이어서 다른 작업을 처리하라는 메세지를 전달한다. 이러한 방식은 요청이 끝날 때까지 무작정 대기를 해야하는 동기 통신보다 빠른 성능을 기대할 수 있다.
 


