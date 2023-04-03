객체와 배열의 주요 기능 ... 
==================
```
// 단축 속성명
const name = 'mike';
const obj = {
    age:21,
    name, 
    getName() {
        return this.name;
    },
} ;
-> 
const name = 'mike';
const obj = {
    age:21,
    name: name, 
    getName: function getName() {
        return this.name;
    },
} ;

console.log({name, age})
=> console.log('name= ', name, ', age= ', age);

```
- 계산된 속성명( computed property names )
```
function makeObject1(key, value){
    const obj = {};
    obj[key] = value;
    return obj;
}

function makeObject2(key, value){
    return { [key]: value};
}
```

- 전개 연산자 ( spread operator)
```
Math.max(1, 3, 7, 9);
const numbers = [1, 3, 7, 9];
Math.max(...numbers);
```

# 비구조화 문법 (destructuring)

```
// 배열 비구조화
const arr = [1, 2];
const [a, b] = arr;

// 비구조화 문법, 기본값 정의
cosnt arr = [1];
const [a=10, b=20] = arr;
// 출력 a = 1,, b = 20, //

// swap
let a = 1;
let b = 2;
[a, b] = [b, a];

// 배열 component 선택
const arr = [1, 2, 3];
const [a, , c] = arr;
a = 1, c = 3;

// ...leftover
const arr = [1, 2, 3];
cost [first, ...rest1] = arr;
rest1 = [2, 3];

const [a, b, c, ...rest2] = arr;
rest2 = [];

```

# optinal chaining

```
// 객체의 null, undifined 확인 후 초기화
const person = null;
cosnt name = person && person.name;
cosnt name2 = person?.name; // person 
=== const name = person === null || person === undefined ? undifined : person.name;

// 함수에서도 사용 가능 
const person ={
    getName: ()=> 'abc';
}
const name = person.getName?.();

```