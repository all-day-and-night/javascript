Generator
=========

> 함수의 실행을 중간에 멈추고 재개할 수 있는 기능

```
functin* f1(){
    yield 10;
    yield 20;
    return 'finished';
}
const get = f1();
```

- next method
```
function* f1(){
    console.log('f1-1');
    yield 10;
    console.log('f1-2');
    yield 20;
    console.log('f1-3');
    return 'finished';
}

const get = f1();
console.log(get.next()); // 1번째 yield 까지 실행 done: false
console.log(get.next()); // 2번째 yield 까지 실행 done: false
console.log(get.next()); // done True

get.return('abc') // 멈췄던 곳에서 실행을 그대로 종료 
get.throw('error') // 예외 발생으로 인식 try catch 사용 가능

function* f1() {
    try{
        console.log('f1-1');
        yield 10;
        console.log('f1-2');
        yield 20;
    } catch(e) {
        console.log('f1-catch', 2);
        yield 30;
        console.log('f1-3');
        yield 40;
        contole.log('f1-4');
    }
}
```

# iterable, iterator

- iterator 조건
1. next 메서드
2. next 메서드는 value, done 속성값을 가친 객체 반환
3. done 속성값은 작업이 끝났을 때 참

- iterable 조건
1. Symbol.iterator 속성값으로 함수를 갖고 있다.
2. 해당 함수를 호출하면 iterator를 반환한다. 

> 배열의 경우
```
const arr = [10, 20, 30];
const iter = arr[Symbol.iterator]();
console.log(iter.next());
```

# Generator를 활용한 map, filter, take

> 새로운 배열 객체를 생성하지 않기 때문에 메모리 효울적 
> 필요한 연산만 수행 
```
// map
function* map(iter, mapper){
    for(const v of iter){
        yield mapper(v);
    }
}

//filter
function* filter(iter, test){
    for (const v of iter){
        if (test(v)){
            yield v;
        }
    }
}

//take
function take(n, iter){
    for (const v of iter) {
        yield v;
        if(--n <= 0) return;
    }
}

```

- yield
```
yield* ==
for (const value of [a, b, ...c]){
    yield value;
}
```

- 인자로 받는 yield
```
function* f1(){
    const data1 = yield;
    console.log(data1);
    const data2 = yield;
    console.log(data2);
}
const gen = f1();
gen.next();

```