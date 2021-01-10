## Database

### Index

1. 데이터 베이스란?
2. [Relational Database](#relational-database)
3. [데이터 베이스 용어 정리](#데이터-베이스-용어-정리)

---

과제할 때 썼던 membes.js 처럼 필요한 데이터들을 **변수**에 저장했었는데, 이렇게 되면 서버가 재시작할 때마다 데이터들이 리셋된다. 😂

**solution** 👉🏻 **데이터베이스**를 사용해서 데이터를 관리한다.

---

### 데이터 베이스란?

- 관련성을 가지며 중복이 없는 **데이터의 집합**
- 이런 DB를 관리하는 시스템을 **DBMS**라고 부름.
- 다수의 사용자가 사용하는 데이터들의 공유와 운영을 위해 사용한다.

---

### Relational Database

> 관계형 데이터 베이스

키와 값들의 간단한 관계를 **테이블화** 시킨 매우 간단한 원칙의 전산정보 데이터베이스.

키: `idx`, `Name`, `Part`, `Age`

값: 최영훈, 서버, 21 ...

| idx  | Name   | Part | Age  |
| ---- | ------ | ---- | ---- |
| 0    | 최영훈 | 서버 | 26   |
| 1    | 윤가영 | 서버 | 21   |
| 2    | 이다은 | IOS  | 21   |

### 데이터 베이스 용어 정리

#### Attributes, column : 속성

: 위의 테이블에서 `idx`, `Name`, `Part`, `Age` 가 속성이다.

#### Tuple, Row: 행

: 위 테이블에서 행 한 줄을 row(tuple)라고 한다.

#### Primary Key (기본키)

- 다른 데이터와 **구별**할 수 있는 식별자
- 한 테이블에는 한 개 이상의 Primary key 가 있어야한다!
- `Not null`, `unique`

#### Index

- 데이터의 색인 기능 (분류 목적)
- 관계형 데이터베이스에서 **검색 속도**를 높이기 위한 도구
- `unique`할 경우 기본키로 사용되는 경우가 많다. 

#### Foreign Key (외래키)

: 한 테이블의 Column 중 다른 테이블의 row(데이터 하나)를 식별할 수 있는 Key

[`USER` table]

| idx  | Name   | IdNumber       |
| ---- | ------ | -------------- |
| 0    | 류세화 | 990226-xxxxxxx |
| 1    | 안재은 | 971113-xxxxxxx |
| 2    | 최예진 | 980718-xxxxxxx |

[`EMAIL` Table]

**여기서 `userIdx` 이 외래키!** `USER` 테이블의 row(사람)를 식별할 수 있게 한다.

| idx  | userIdx | Email              |
| ---- | ------- | ------------------ |
| 0    | 0       | tpghk3tp@naver.com |
| 1    | 0       | tpghkRyu@gmail.com |
| 2    | 1       | jeunao@naver.com   |
| 3    | 1       | jeunaaaa@gmail.com |
| 4    | 1       | jeun@kakao.com     |
| 5    | 2       | dPwls@daum.net     |

