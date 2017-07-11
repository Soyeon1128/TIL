
# 즉시 실행 함수 (IIFE, Immediately-invoked function expression)

```javascript
(function(){}());
(function(){})();
```

```javascript
// 객체 값을 변수에 참조한 예
var memorial_card = {};

// IIFE 패턴을 사용하여 실행된 결과 값 객체를 반환 받은 변수 예
var another_memorial_card = (function(){
  return {};
}());
```
