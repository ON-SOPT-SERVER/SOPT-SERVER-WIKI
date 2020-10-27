# NodeJS 정리

## 목차
1. [NodeJS란](#nodejs-is) (작성자: 김우영)
2. [NodeJS의 특징](#characteristics)

    2.1 [Non-Blocking I/O](#non-blocking)

    2.2 [Single Thread](#single-thread)

    2.3 [Event-Driven](#event-driven)

3. [NodeJS의 장점](#pros) (작성자 : 이영은)
4. [NodeJS의 단점](#cons)
5. [NodeJS로 할 수 있는 것](#what-we-can-do)



## 1. NodeJS란 <a name="nodejs-is"></a>
NodeJS는 자바스크립트를 웹브라우저 외부에서 실행할 수 있게 만들어주는 런타임 환경입니다.\
본래 자바스크립트는 웹브라우저 내부에서만 사용할 수 있었는데, NodeJS의 등장으로 인해 이제 그 외부에서도 자바스크립트를 사용할 수 있게 되었습니다. 이로 인해 클라이언트 쪽에서만 사용되는 언어였던 자바스크립트를 통해 서버를 구축할 수 있게 되었습니다.

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

**2.2.1 Single Thread란**

```
Single Thread란 하나의 Thread만 사용하여 여러 client로 부터 오는 Req를 처리하는것

client의 요청이 들어오면 thread는 CPU작업을 하다가 IO작업을 하고 그동안 다른 client의 요청을 받아서 실행시켜준다.

EX) A고객이 카운터에게 팥빙수를 주문하면 바리스타는 팥빙수를 만든다. 그 와중에 B고객이 카운터에서 아이스아메리카노를 주문하면 카운터에서 주문을 받고 팥빙수를 만들면서 아이스아메리카노를 내린다. 하지만 아이스아메리카노가 더 빨리 만들수있기 떄문에 B고객의 아이스아메리카노가 먼저나오고 팥빙수가 나중에 나온다.  

작업을 요청한 순서와 반환되는 순서는 일치하지 않을수 있다!
```

**2.2.2  노드는 Multi Tread???**

```
Node.Js는 single thread뿐만 아니라 내부적으로 multi thread pool을 사용한다.
이는 '너무 많은 CPU'를 사용하는 작업이나 '대용량 파일을 처리'시에 Non Blocking이
에러를 발생하게 되고 node자체가 다운될수 있다. 이떄는 thread pool에서 대기하고 있던 thread를 이용하여 blocking을 막아줄수있다.

참고로 노드의 multi thread pool에서 thread를 강제로 뽑아서 노드를 multi thread로 사용해줄수 있지만.. 노트북이 히터가 될수 있다!
```



### &ensp; 2.3 Event-Driven <a name="event-driven"></a>

## 3. NodeJS의 장점 <a name="pros"></a>

* Single Thread, 비동기 I/O 처리에 기반하여 높은 성능을 가진다.
* File I/O와 네트워크 처리를 이벤트 드리븐 방식으로 처리하여 빠른 처리가 가능하다.
* CPU 대기시간을 최소화 할 수 있다.
* CPU 부하가 적고, 많은 커넥션을 동시에 처리하는 구조에 적합하다.
* JavaScript를 이용하기 때문에 프론트엔드 개발자의 진입장벽이 낮다.
* Non-blocking I/O와 Single Thread 이벤트 루프를 통한 높은 Request 처리 성능을 가진다.
```
Non-blocking I/O는 비동기 처리를 실시하므로 데이터베이스 처리와 웹 페이지 표시를 별도 진행한다.
```
* SocketIO라는 실시간 통신을 실현하는 라이브러리 사용으로 대량의 데이터 처리와 실시간 통신을 구현할 수 있다.


## 4. NodeJS의 단점 <a name="cons"></a>

## 5. NodeJS로 할 수 있는 것 <a name="what-we-can-do"></a>

