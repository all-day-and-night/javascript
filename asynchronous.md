Asynchronous 비동기
=================

# Promise

```
function requestData(callback) {
    setTimeout(() => {
        callback({name: 'abc', age: 23});
    }, 1000);
}

function onSuccess(data){
    console.log(data);
}

console.log('call requestData');
requestData(onSuccess);

// Promise로 변환
requestData1()
    .then(data => {
        console.log(data);
        return requestData2();
    })
    .then(data => {
        console.log(data);
    })
// promise를 사용하면 비동기 함수를 동기 + 순차적 프로그래밍 가능

```

## Promise 객체 사용
```
const p1 = new Promise((resolve, reject) => {});
const p2 = Promise.reject('error message');
const p3 = Promise.resolve(param);
```

- Promise 객체의 상태
1. 대기중(pending)
2. 성공(fulfiiled)
3. 실패(reject)

```
// Promise + then()
requestData().then(onResolve, onReject); // 성공시 onResolve, 실패시 onReject
Promise.resolve(123).then(data => console.log(data));
Promise.reject('error').then(null, data => console.log(data));

```
- then() 은 Promise 객체 반환
```
requestData1()
    .then(data => {
        console.log(data);
        return requestData2();
    })
    .then(data => {
        console.log(data);
        return data + 1;
    })
    .then(data => {
        console.log(data);
        throw new Error('some error');
    }) // 위에서 error 발생 시 다음 then에서 2번째 함수 실행
    .then(null, error => {
        console.log('error');
    }) // 아무런 return 값이 없기 때문에 undifined 값을 갖고 있는 Promise 객체 리턴 
    .then(data => {
        console.log(data);
    })
```

- Promise.reject('error')
```
Promise.reject('err')
    .then(() => console.log('then 1')) // 2번 째 함수가 정의되지 않았기 때문에 reject 객체 그대로 반환 / 출력 x
    .then(() => console.log('then 2')) // 마찬가지 / 출력 x 
    .then(
          () => console.log('then 3'),
          () => console.log('then 4'), // reject 객체이므로 2번째 함수 호출
          )
    .then(
          () => console.log('then 5'), // 위의 return 값이 error가 없기 때문에 1번째 함수 호출
          () => console.log('then 6'),
        );

``` 

- Promise.reject().catch 
> 오류 상황시 Promise 객체 처리를 위해 사용 

```
Promise.reject(1).then(null, error => {
    console.log(error);
});
Promise.reject(1).catch(error => {
    console.log(error);
})

Promise.resolve().then(
    () => {
        thrown new Error('some error');
    },
    error => {
        console.log(error);
    }
). then(onResolve, onReject);
// 위 코드는 다음과 같이
Promise.resolve()
    .then(() => {
        throw new Error('some error')
    })
    .catch(error => {
        console.log(error);
    });
// 코드의 가독성 높임

// catch이후에도 then 사용 가능 / 오류 발생 시 정상 흐름으로 처리 가능
Promise.reject(10)
    .then(data => { // 2번째 함수 x Promise reject 객체 그대로 반환
        console.log('then1: ',data);
        return 20;
    })
    .catch(data => { // 반환된 객체에서 data 10
        console.log('catch:', data);
        return 30;
    })
    .then(data => { catch 후 정상 흐름 30 출력  
        console.log('then2:', data);
    })
```

- Promise finally
```
// fulfilled, reject 상태에서 모두 수행 
// 데이터가 넘어오지 않음, 이전에 있던 객체 그대로 반환 
Promise.resolve(10)
    .then(data => {
        console.log('onThen', data);
        return data + 1;
    })
    .catch(error => {
        console.log('onCatch');
        return 100;
    })
    .finally(() => {
        console.log('onFinally');
    })
    .then(data => {
        console.log('onThen', data);
        return data + 1;
    })
```

- api 호출시 예
```
function requestData(){
    return fetch()
        catch(error => {

        })
        .finally(() => {
            sendLogToServer('requestData finished');
        });
}
requestData().then(data => console.log(data));
```


# 병령 수행
```
requestData1().then(data => console.log(data));
requestData2().then(data => console.log(data));


// Promise 객체를 활용한 병렬처리
// 입력한 모든 함수가 fulfilled 상태가 되어야 Promise.all도 fulfilled 리턴 
Promise.all([requestData1(), requestData2()]).then(([data1, data2]) => {
    console.log(data1, data2);
});
```

# Promise.race
> 입력된 함수중 가장 빠르게 settlede된 Promise 객체의 상태를 반환 
```
Promise.race([
    requestData(),
    new Promise((_, reject) => setTimeout(reject, 3000)),
])
    .then(data => console.log('fulfilled', data))
    .catch(error => console.log('reject'));
```

# Promise 객체를 사용한 caching
> pending 상태가 아닌 fulfilled, reject 상태에서는 객체의 상태 변화 x
> 이러한 성질로 caching 기능 구현

```
let cachedPromise;
function getData(){
    cachedPromise = cachedPromise || requestData();
    return cachedPromise;
}
getData().then(v => console.log(v));
getData().then(v => console.log(v));
```

# 간단한 오류 해결

1. undefined 발생시 
> return 빼먹었..?

2. 예상한 반환 값과 다를 경우
> then은 Promise 객체를 변경하지않고 새로 생성해서 사용
> return P.then()을 기본으로 사용하자 

3. 중첩해결
> 가독성이 좋게 then(return --).then(return -- ).then(return --) 식으로 사용하자 

4. 인자 2개 사용할 경우
> Promise all 사용
```
requestData()
    .then(result1 => {
        return Promise.all([result1, requestData2(result1)])
    })
    .then(([result1, result2]) => {
        //...
    });
```

5. 비동기 함수 사용시 오류 처리
> then(async()).catch()

# Async Await
> 비동기 프로그래밍을 동기 프로그래밍으로 사용할 때 사용 
```
async function getData(){
    return 123;
}
getData().then(data => console.log(data));
```

> async 함수는 Promise 객체 반환할 수 있음
```
async function dataData(){
    return Promise.resolve(123);
}
getData()
    .then(data => console.log('fulfilled'), data) // 출력
    .catch(data => console.log('rejected'), data);
```

> await 키워드 사용

```
function requestData(value){
    return new Promise(resolve => 
        setTimeout(() => {
            console.log('requestdata:', value);
            resolve(value);
        }, 1000),
    );
}
async function printData(){
    const data1 = await requestData(10);
    const data2 = await requestData(20);
    console.log(data1, data2); 
}
```
> await은 Promise 객체가 settled 된 후 데이터 값 저장 
> 동기 프로그래밍 방식으로 코드 작성 가능 

```
async function getData(){
    console.log('getData1');
    await Promise.reject();   // 이 부분에서 rejected Promise 객체 반환 아래 코드 수행 x
    console.log('getData2');
    await Promise.resolve();
    console.log('getData3);
}
getData()
    .then(() => console.log('fulfiiled'))
    .catch(error => console.log('error')) // reject에서 종료되었기 때문에 error 
```

> await 키워드는 async 함수 내부에서만 사용 가능 

> async await vs then

```
// then
function getDataPromse() {
    return asyncFunc1()
        .then(data1 => Promise.all([data1, asyncFunc2(data1)]))
        .then(([data1, data2]) => {
            return asyncFunc3(data1, data2);
        })
}

// async await
async function getDataAsync() {
    const data1 = await asyncFunc1();
    const data2 = await asyncFunc2(data1);
    return asycnFunc3(data1, data2);
}
```

# async await 병렬 처리

```
async function getData(0}{
    const p1 = asyncFunc1();
    const p2 = asyncFunc2();
    const data1 = await p1;
    const data2 = await p2;
    console.log({ data1, data2 });
})
// 두 함수 사이에 종속성 x일 경우 

// Promise.all 사용
const [data1, data2] = await Promise.all([asyncFunc1(), asyncFunc2()]); 
```
# async await 예외처리

```
async function getData(){
    try{
        await doAsync();
        return doSync();
    } catch(error){
        console.log(error);
        return Promise.reject(error);
    }
}

// Thenable 사용

class ThenableExample {
    then(resolve, reject) {
        setTimeout(() => resolve(123), 1000);
    }
}

async function asyncFunc() {
    const result = await new ThenableExample();
    console.log(result); 
}
asyncFunc();
```

