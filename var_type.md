# Var의 문제점

- ES6 
> const, let 사용가능

## var
> 함수 내에서 선언될 때는 함수 범위
> 함수 바깥에서 선언시 전역변수 
> 재선언, 업데이트 가능
> hoisting / 초기화 전에는 undifined

## Let
> {} 블록 범위로 바인딩, 외부에서 사용 불가능
> 업데이트 가능 / 재선언 불가능
> hoisting되지만 초기화 이전에 let 변수 사용시 Reference Error(참조 오류 발생)

## Const 일정한 상수값 유지
> 선언된 블록 범위 내에서만 접근 가능 
> 업데이트, 재선언 불가능 
> 객체의 속성은 업데이트 가능 
> let과 마찬가지로 hoisting되지만, 초기화 이전에 사용시 Reference Error




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

# Boolean Type, nullish coalescing

> true, false

```
// && ,||, !, ~ 

// nullish coaleascing
// 빈 문자열도 기본값으로 사용하고 싶다면 사용, 아니면 or 연산자 사용
const name = person.name ?? 'unknown';
const name = 
    person.name === undifined || person.name === null ? 'unknown' : person.name;
```

# Object Type, Array

```
const Obj = {
    age: 21,
    name: 'mike'
};

const Obj2 = new Object({
    age:21,
    name:'mike'
});
// 생성자를 활용한 기능 사용
Object.keys(Obj);
Object.values(Obj);
Object.entries(Obj);

for (const [key, value] of Object.entries(Obj)){
    console.log(key, value);
}

const Obj = {
    age: 21,
    name: 'mike'
};
// key, value 추가
Obj.city = 'seoul';
//삭제
delete Obj.city;
delete Obj['city'];
```

- Array
```
const arr = [1, 2, 3];
const arr2 = new Array(1, 2, 3);

typeof arr === 'object';

//iterator
arr.map(item => item + 1);
arr.filer(ite => item >= 2);
arr.redurce((acc, item) => acc + item, 0);

arr.forEach(item => console.log(item));
for (const item of arr){
    console.log(item);
}
arr.some(item => item === 2); // 하나라도 2가 있으면 true
arr.every(item => item === 2); // 모든 item이 2이면 true
arr.includes(2);
arr.find(item => item % 2 === 1)
arr.findIndex(item => item % 2 === 1);

// push, pop
arr.push(4)
arr.pop();

// splice()
arr.splice(1, 1); // 1번 인덱스에서 1개 삭제
arr.splice(1, 0, 10, 20, 30); // 1번 인덱스에서 0개 삭제 후 10, 20, 30 추가
arr.splice(1, 3, 40, 50); // 1번 인덱스에서 3개 삭제 후 40, 50 추가 

// 정렬
arr.sort()
```



