# NodeJS 정리

## 목차
1. [NodeJS란](#nodejs-is)
2. [NodeJS의 특징](#characteristics)

    2.1 [Non-Blocking I/O](#non-blocking)

    2.2 [Single Thread](#single-thread)

    2.3 [Event-Driven](#event-driven)

3. [NodeJS의 장점](#pros)
4. [NodeJS의 단점](#cons)
5. [NodeJS로 할 수 있는 것](#what-we-can-do)



## 1. NodeJS란 <a name="nodejs-is"></a>
NodeJS는 자바스크립트를 웹브라우저 외부에서 실행할 수 있게 만들어주는 런타임 환경입니다.\
본래 자바스크립트는 웹브라우저 내부에서만 사용할 수 있었는데, NodeJS의 등장으로 인해 이제 외부에서도 자바스크립트를 사용할 수 있게 되었습니다.

## 2. NodeJS의 특징 <a name="characteristics"></a>

### &ensp; 2.1 Non-Blocking I/O <a name="non-blocking"></a>
* 동기(Blocking, Sync) : 요청을 하고 완료를 할 때까지 기다리는 방식

* 비동기(Non-Blocking, Async) : 방식은 요청을 하고 바로 제어권을 돌려 받는 방식 즉 요청을 하고 다시 프로그램을 처리하다가 완료 이벤트가 발생하면 미리 지정한 처리를 진행한다.

#### 자바스크립트에서 비동기 처리방법

**2.1.1 Callback Function**
* Callback 함수: 어떤 이벤트가 발생했거나 특정 시점에 도달했을때 시스템에서 **호출**되는 함수
자바스크립트 함수 → 다른함수의 파라미터로 전달가능

*비동기식 callback*
```
console.log('Hello');

setTimeout(function () {
    console.log('Bye');
    }, 3000)
    
console.log('Hello again);
```
\
**2.1.2 Promise**
* Promise: ES6에서 비동기 처리위해 도입

*Promise의 3가지 상태*
```
✔️ Pending: 최초 생성돼 비동기 작업 수행중인 상태
✔️ Fullfilled: 비동기 작업이 성공적으로 완료된 상태
✔️ Rejected: 비동기 작업이 실패한 상태
```
\
**2.1.3 Async/await**
* Async/await: 동기적인 코드처럼 직관적으로 볼 수 있음
* async: 함수앞에 async 붙히면 암묵적으로  promise 반환
* await: promise를 기다림, async로 정의된 함수에서만 사용가능

### &ensp; 2.2 Single Thread <a name="single-thread"></a>

### &ensp; 2.3 Event-Driven <a name="event-driven"></a>

## 3. NodeJS의 장점 <a name="pros"></a>

## 4. NodeJS의 단점 <a name="cons"></a>

## 5. NodeJS로 할 수 있는 것 <a name="what-we-can-do"></a>

