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
```
// number, bigint, string, boolean, object, symbol, undefined, null
```


# Number

- 문자열에서 숫자 파싱하기
```
Number.parseInt('---')
Number.parseFloat('---')

const v = Number.parseInt('abc');
console.log(v) // NaN 출력 

const v = 1 / 0; // Infinity 출력 
console.log('Infinity', v === Infinity);
console.log('Number.isFintie', Number.isFinite(v));
```

- number -> 64 비트 부동소수점 사용 , 최적화 불가



# string 
```
// 선언 방식 
cost s1 = 'abc';  
cost s2 = "abcd";
cost s3 = `abc`;

// s1.length // 길이 정보 추출 가능
```

> 문자열 생성
```
const name = 'mike';
const age = 23;
const text1 = 'name: ' + name + ', age: ' + age;
cosnt text2 = `name: ${name}, age: ${age}`; // 백틱 사용
```

> javascript string은 불변 / 초기화 후 변경 x

```
const input = 'This is my car. The car is mine';
const output = input.replace('car', 'bike');
const output = input.replaceAll('car', 'bike');

// string 불변이기 때문에 새로운 문자열 객체 생성 

s1.includes('car');
s1.startsWith('car');
s1.endsWiths('car');

// 문자열  추출
s1.substr(0, 11); // (시작점, offset)
s1.slice(0, 2); // (시작점, 끝점)

// index 반환
s1.indexOf(' ') 

// 분할
s1.split(' ');

// 합침
s1.split(' ').join('');

// trim 앞뒤 공백제거
arr.map(item => item.trim());

// 일정 길이 
'123'.padStart(5, '0');
'123'.padEnd(5, '0');
```



