# Var의 문제점

- ES6 
> const, let 사용가능

> 정의된 변수는 함수 스코프를 갖기 때문에 함수 내에서만 사용 가능

```
function example() {
    var i = 1;
}
console.log(i);
// Reference Error 발생

for (var i = 0; i < 10 ; i++){
    console.log(i);
}
console.log(i);
// 함수가 종료되어도 마지막 값이 i에 남아있음

//즉시 실행 함수 사용
(for (var i = 0; i < 10 ; i++){
    console.log(i);
})(); // 외부에서 접근 x

// Hoisting
// 변수를 정의하기 전에 사용해도 에러 x / 사용가능하지만 할당 이전이기 때문에 undifined 
console.log(myVar)
var myVar = 1;

// Hoisting 2
console.log(myVar);
myVar = 2;
console.log(myVar);
var myVar = 1;

// 재정의 가능
// 재할당 가능 
```

# Const, Let

> Block Scope
> 선언된 블록 바깥에서 사용 불가능 

```
if(true) {
    const i = 0;
}
console.log(i); // error

//Hoisting
console.log(foo)
const foo = 1;
// hoisting이 되지만 var와 차이점은 호이스팅 후 undifined가 아니라 아무값도 할당받지 않는다는 점

```



# 자바스크립트의 8가지 기본타입
// number, bigint, string, boolean, object, symbol, undefined, null
```
