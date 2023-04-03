Function
==========

 > js 에서 함수는 변수에 담아 사용가능 하기 때문에 일급 함수이다

 ```
const add10 = function(a){
    return a + 10;
}

function apply(arr, op){
    return arr.map(op);
}

apply([1, 2, 3], add10);
```

- call stack(stack)
- execution context
- lexical environment(map)

# 함수 정의 방법
```
function printLog(a = 1) {
    console.log({ a });
} // arg를 받지만 default value는 1


// default value에 함수 
function getDefault(){
    return 1;
}

function printLog(a = getDefault()) {
    console.log({ a });
}

// 반드시 값을 입력해야 하는 경우에 customizing 가능 

// ...rest // 나머지 매개변수
function printLog(a, ...rest){
    console.log({ a, rest });
}
printLog(1, 2, 3);
>> { a:1, rest: [2, 3]}

// 명명된 매개변수
function getValues({ numbers, greaterThan, LessThan }) {
    return numbers.filter(item => greaterThan < item && item < lessThan);
}

const numbers = [10, 20, 30, 40, 50];
const result = getValues({ numbers, greaterThan: 5, lessThan: 25});

// arrow function
const add = (a, b) => a + b;
const addAndReturnObject = (a, b) => ({ result: a + b });
```

# this
```
function Counter() {
    this.value = 0;
    this.add = amount => {
        this.value += amount
    }
};

const counter = new Counter();
console.log(counter.value);
counter.add(5);
console.log(counter.value);

vs 
function Counter() {
    this.value = 0;
    this.add = function(amount) {
        this.value += amount
    }
};

const counter = new Counter();
console.log(counter.value);
counter.add(5);
console.log(counter.value);
const add = counter.add;
add(5);
// 일반 함수로 생성된 add는 생성될 당시의 this 객체를 바라보지 않기 때문에 전역 변수에 접근, 사용하고자 하는 기능과 상이 

```