### 📌 Index

1. [Sequelize Query](#sequelize-query) 💖
2. [시퀄라이즈 쿼리 실습!](#실습) 💥
   1. [Create](#1.-생성:-create)
   2. [findOne](#2.-fineOne)
   3. [findAll](#3.-findAll)
   4. [Update](#4.-update)
   5. [Destroy](#5.-destroy)

---

## Sequelize Query

시퀄라이즈 쿼리를 이용해서 CRUD 작업을 진행한다.

| Action   | SQL    | Sequelize Query |
| -------- | ------ | --------------- |
| 생성     | INSERT | create          |
| 조회     | SELECT | find            |
| 업데이트 | UPDATE | update          |
| 삭제     | DELETE | destory         |

---

### 실습

실습해볼 Table은 다음과 같다!

Sequelize Model: `User`

MySQL Table: `users`

| Id   | name   | age  | address    |
| ---- | ------ | ---- | ---------- |
| 0    | 이현주 | 24   | 진주시     |
| 1    | 최다인 | 23   | 서울특별시 |
| 2    | 임찬기 | 24   | 서울특별시 |

---

### 1. 생성: create

#### SQL에서는 이렇게 했었는데

```sql
INSERT INTO users (name, age, address) VALUES ('윤가영', 21, '서울특별시');
```

#### Sequelize Query

```javascript
const { User } = require('models/index.js가 정의된 상대경로');
const user = await User.create({
    userName: '윤가영',
    age: 21,
    address: '서울특별시',
});
```

Sequelize는 자체적으로 promise를 반환한다. 👉🏻 `async`/`await` 사용 가능!

---

### 2. findOne

첫 번째 예시: **조건 없이 row 하나 가져오기**

#### SQL - SELECT, LIMIT

```sql
select * from users LIMIT 1;
```

#### Sequelize query  - readOne()

```javascript
const { User } = require('models/index.js가 정의된 상대경로!');
const user = await User.readOne({ });
```

결과는 

| Id   | name   | age  | address |
| ---- | ------ | ---- | ------- |
| 0    | 이현주 | 24   | 진주시  |

두 번째 예시: **name이 임찬기인 row 가져오기**

#### SQL - SELECT/WHERE

```sql
select * from users WHERE name = '임찬기';
```

#### Sequelize query  -findOne

```javascript
const { User } = require('models/index.js가 저의된 상대경로!');
const user = await User.findOne({
    where: {
        name: '임찬기',
    },
});
```

결과는

| Id   | name   | age  | address    |
| ---- | ------ | ---- | ---------- |
| 2    | 임찬기 | 24   | 서울특별시 |

---

### 3. findAll

첫 번째 예시: **조건 없이 모두 가져오기**

#### SQL - SELECT

```sql
select * from users;
```

#### Sequelize query - findAll()

```javascript
const { User } = require('models/index.js가 정의된 상대경로');
const users = await User.findAll({ });
```

#### 결과

| Id   | name   | age  | address    |
| ---- | ------ | ---- | ---------- |
| 0    | 이현주 | 24   | 진주시     |
| 1    | 최다인 | 23   | 서울특별시 |
| 2    | 임찬기 | 24   | 서울특별시 |
| 3    | 윤가영 | 21   | 서울특별시 |

두 번째 예시: **address가 서울특별시인 row만 가져오기**

#### SQL - SELECT/WHERE

```sql
select name, address from users whrer address = '서울특별시';
```

#### Sequelize query

```javascript
const { User } = require('models/index.js가 정의된 상대경로!');
const users = await User.findAll({
    attributes: ['name', 'address'], // attributes 배열을 넣어 원하는 컬럼값만 뽑아 올 수 있음
    where : {
        address: '서울특별시'
    }
});
```

#### 결과

| name   | address    |
| ------ | ---------- |
| 최다인 | 서울특별시 |
| 임찬기 | 서울특별시 |
| 윤가영 | 서울특별시 |

세 번째 예시 - **특수연산으로 조건 걸어 조회**

Sequelize 객체 내부에서 Op 객체를 불러와 특수 연산을 사용할 수 있다.

- `Op.gt`: greater than 초과
- `Op.gte`: greater than or equal
- `Op.lt`: less than
- `Op.lte`: less than or equal
- `Op.ne`: not equal
- `Op.or`: 또는
- `Op.in`: 배열 요소 중 하나
- `Op.notIn`: 배열 요소와 모두 다름

#### SQL

```sql
select age, name from users where age > 21;
```

#### Sequelize query

```javascript
const { Op } = require('sequelize'); //Op 객체 불러오기!
const { User } = require('models/index.js가 정의된 상대경로!');
const users = await User.findAll({
    attributes: ['age', 'name'],
    where: {
        age: { [Op.gt]: 21 }, // 나이가 21 초과인 row를 조회
    }
});
```

#### 결과

| age  | name   |
| ---- | ------ |
| 24   | 이현주 |
| 23   | 최다인 |
| 24   | 임찬기 |

---

### 4. UPDATE

### SQL

```sql
update users set name = '바꿀 이름' where id = 2;
```

#### Sequelize query

```javascript
const { User } = require('models/index.js가 있는 상대경로');
const user = await User.update({ name: '바꿀 이름' }, {
    where: {
        id: 2,
    },
});
```

#### 결과 (모든 row 조회 시)

| id   | name          | age  | address    |
| ---- | ------------- | ---- | ---------- |
| 0    | 이현주        | 24   | 진주시     |
| 1    | 최다인        | 23   | 서울특별시 |
| 2    | **바꿀 이름** | 24   | 서울특별시 |
| 3    | 윤가영        | 21   | 서울특별시 |

---

### 5. destroy

#### SQL

```sql
delete from users where id = 2;
```

#### Sequelize query

```javascript
const { User } = require('models/index.js가 정의된 상대경로');
const user = await User.destroy({
    where: {
        id: 2,
    },
});
```

---

더 자세한 쿼리 예제 : https://sequelize.org/master/manual/model-querying-basics/html

