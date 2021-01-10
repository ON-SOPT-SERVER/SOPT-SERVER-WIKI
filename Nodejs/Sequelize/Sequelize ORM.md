### Index

1. [Sequelize ORM](#sequelize-orm)
2. [ORM의 장점](#orm-사용-시-장점)
3. [ORM의 단점](#)(#orm-사용-시-단점)
4. [SQL과 ORM 비교](#sql과-orm-비교)

---

## Sequelize ORM

- NodeJS에서 가장 많이 사용되는 ORM이다.
- 자바스크립트의 객체와 데이터베이스의 Relation을 매핑해주는 역할을 한다.

- MySQL, PostgreSQl, MariaDB, SQLite, MSSQL 을 지원
- ✨ Promise 를 기본으로 지원해준다 ✨

---

sequelize는 ORM 중에 하나인데, ORM을 사용할 때의 장단점을 보자

### ORM 사용 시 장점

- 재사용 및 유지보수의 편리성 증가

- 특정 DBMS에 종속되지 않는다.
- SQL문이 코드에 들어가지 않아 코드가 깔끔해짐
- Injection을 막아줌
- ORM이 nesting 데이터를 바인딩해준다.

### ORM 사용 시 단점

- 사용은 편하지만 설계에 신중해야한다. 👉🏻 잘못 구현할 경우 속도 저하 및 일관성이 무너지는 문제 발생.
- 프로시저가 많은 DB 환경에서는 ORM의 객체 지향적인 장점을 활용하기 어렵다.
- 프로젝트의 복잡성이 높아질 경우 ORM만 사용해서 구현하기 어려워진다.



대충 정리하면, 너무 복잡한 DB를 설계하는 게 아니면 Sequelize를 사용하는 것이 편한 방법이라는 것 같다.

---

### SQL과 ORM 비교

- Connection Pool 을 생성해서 SQL을 사용한 예시!

  ```javascript
  createPost: async (writerIdx, title, content, createdAt) => {
      const fields = `writerIdx, title, content, createdAt`;
      const question = `?,?,?,?`;
      const values = [writerIdx, title, content, createdAt];
      const query = `INSERT INTO ${table}(${fields}) VALUES(${question})`;
      try {
          const result = await pool.queryParamArr(query, values);
          const insertId = reault.insertId;
          return insertId;
      } catch (err) {
          if (err.errno == 1062) {
              console.log('Create posting ERROR: ', err.errno, err.code);
              return -1;
          }
          console.log('Create posting ERROR: ', err);
          throw err;
      }
  }
  ```

  

- ORM을 이용해서 CREATE 사용 예시 👍🏻

  ```javascript
  module.exports.create = async ({ groupLocation, groupName, etc }) => {
  	const dtcData = _.isNil(etc) ? '' : etc;
      try {
          const group = await Group.create({ 
              groupLocation,
              groupName,
              etc: etcData,
          });
          return group;
      } catch (err) {
          throw err;
      }
  }
  ```

