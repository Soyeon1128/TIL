
# 재귀함수 / 팩토리얼
## 재귀함수란 ? 
> 자기 자신을 재호출 하는 함수를 말한다. (ex : 팩토리얼 )
### 예시
``` javascript
function add(){
    add();
}
```
## 팩토리얼(Factorial)이란 ?
> 자기 자신의 수에 1 작은 수를 곱하고 또 1작은 수를 곱하고 해서 1작은 수가 1이 될때까지 곱한 값.
### 예시
```
 1! = 1 = 1
 2! = 2 x 1 = 2
 3! = 3 x 2 x 1 = 6
 4! = 4 x 3 x 2 x 1 = 24
 5! = 5 x 4 x 3 x 2 x 1 = 120
```
### 1. 반복문을 이용한 팩토리얼 함수
``` javascript
function factorial(n) {
    // ㅜㅜn<2 인 경우
  if ( n < 2 ) { return 1; }
   // n>=2 인 경우
   // n의 값을 기억하기 위한 result 변수 선언.
   var result = n;
   do { result *= --n; }
   while(n > 1);
   return result;
}
```

### 2. 재귀함수를 이용한 팩토리얼 함수
``` javascript
function factorial(n) {
  if ( n < 2 ) { return 1; }

  // n = 5 인 경우 ,
  //  5 * factorial(4)
  //  5 * 4 * factorial(3) 
  //  5 * 4 * 3 * factorial(2) 
  //  5 * 4 * 3 * 2 * factorial(1)
  // ==> factorial(5) 는 5 x 4 x3 x 2 x 1 이 성립한다.
 return n * factorial(--n);
}
```
 
