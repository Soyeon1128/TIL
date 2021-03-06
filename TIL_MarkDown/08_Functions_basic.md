# 함수

## 함수 선언하기 (호이스팅 주의)

### 1. 함수 식(익명함수)을 변수에 할당(대입) -> 참조
```javascript
// var registerUserInfo = function() {};

var registerUserInfo = function() {
    console.log('registerUserInfo 함수 실행');
};
```

### 2. 함수 이름을 붙여서 선언하기 -> 함수 선언문
```javascript
// function getUserInfo() { }

function getUserInfo() {
    console.log('getUserInfo 함수 실행');
}
```

## 함수 호출하기

- 함수인지 검증 후 실행

### if문 사용
```javascript
if ( isFunction(registerUserInfo) ) {
    registerUserInfo();
}
```

### 논리 연산자 사용
```javascript
isFunction(getUserInfo) && getUserInfo();
```

## 함수 범위

### Global Scope
```javascript
var g_scope = '전역 변수';
```

### Local Scope

- 호이스팅 발생 시 순서
    1)  일단 함수 안에서 찾는다. (지역)
    2)  없으면 다음으로 변수 영역에서 찾는다.
    3)  없으면 다음으로 Parameters(매개변수) 영역에서 찾는다.
    4)  없으면 다음으로 함수를 포함하는 상위 영역에서 찾는다.
    5)  없으면 다음으로 전역에서 찾는다.
    6) 그래도 없으면 ReferenceError 발생!

```javascript
function localScope() {
    console.log('g_scope:', g_scope);

    // 아래의 함수값이 어떻게 나올까?
    innerScopeFn();

    // 1)
    function innerScopeFn() {
        var l_scope = '지역 변수';
        console.log('l_scope:', l_scope);
    }
    // ——> '지역 변수'
    
}
```
```javascript
function localScope() {
    console.log('g_scope:', g_scope);

    // 아래의 함수값이 어떻게 나올까?
    innerScopeFn();

    // 2)
    var innerScopeFn = function() {
         var l_scope = '지역 변수';   
         console.log('l_scope:', l_scope);
    }
    // ——> typeError
    // Why? 함수 표현식은 변수만 호이스팅되기 때문에 innerScopeFn 값은 undefined가 된다.
    // 따라서 innerScopeFn는 함수가 아니게 되므로 실행 시 콘솔에는 typeError가 뜬다.
}
```

