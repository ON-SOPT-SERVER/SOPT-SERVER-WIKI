## Sequelize Model 정의

### 📌 Index

1. [Sequelize Model](#sequelize-model)
2. Model 정의 실습
   1. [define() 으로 모델 정의하기](#model-정의-실습-:-define())
   2. [만든 모델을 Sequelize 객체에 연결하기](#생성한-model을-sequelize-객체에-연결하기)

---

### Sequelize Model

시퀄라이즈의 모델 👉🏻 **데이터베이스의 테이블**을 표현하는 수단

다음은 sequelize모듈의 define() 메소드 정의다.

> `define(modelName: string, attributes: object, obtions: object) : Model`
>
> : Define a new model, **representing a table in the database.**

이처럼 시퀄라에즈에서는 `sequelize.define()` 라는 메서드를 이용해서 테이블을 정의한다.

1. Define model
2. Connect model to sequelize object

---

### Model 정의 실습 : define()

sequelize init 후 생성된 `Models` 폴더에 `[만들고자하는 테이블명].js` 파일을 생성한다.

세미나에서는 `user.js` 로 만들었다.

```javascript
/* Models/user.js */

module.exports = (sequelize, DataTypes) => { // 함수를 export
    // 이
	return sequelize.define('User', {
        email: {
            type: DataTypes.STRING(30),
            unique: true,
            allowNull: false,
        },
        userName: {
            type: DataTypes.STRING(20),
            allowNull: false,
        },
        password: {
            type: DataTypes.STRING(200),
            allowNull: false,
        },
        salt: {
            type: DataTypes.STRING(200),
            allowNull: false,
        },
    }, {
        freezeTableName: true,
        timestamps: false,
    })
}
```

---

### define() 의 attributes 객체

위의 코드에서 attributes 객체를 보면 컬럼들을 정의하고 있다. DataType을 설정할 때 타입이 MySQL이랑 다르니까 밑에 표를 참고하자.

#### Seqeulize Datatype

| MySQL         | Sequelize                   |
| ------------- | --------------------------- |
| VARCHAR(100)  | STRING(100)                 |
| INT           | INTEGER                     |
| TINYINT       | BOOLEAN                     |
| DATETIME      | DATE                        |
| NOT NULL      | allowNull : false           |
| UNIQUE        | unique : true               |
| DEFAULT now() | defaultValue: Sequelize.NOW |

💥 아 그리고! Sequelize에서는 PrimaryKey를 설정해주지 않으면 **자동으로 `id`라는 컬럼의 primarykey 값이 생성된다.**

---

### define() 의 option 객체

위 실습 코드의 option 객체를 보면 아래와 같은 것들이 있다.

- `FreezeTableName`: 이 속성값이 `true`이면 모델명과 DB테이블 이름을 동일하게 설정해준다.

  시퀄라이즈는 기본적으로 모델이름은 단수, 테이블 이름은 복수로 설정한다. 혼란을 막기 위해서 우flsms `true`로 설정 ~ 😏

- `timestamps`: 이 속성은 모델을 정의하고 테이블이 생성되면 자동적으로 createdAt, updatedAt 컬럼이 생성된다. default 값이 `true` 이기 때문에 컬럼이 생기는 것을 원하지 않으면 `false`로 명시.

위에서는 사용하지 않은 또 다른 Model 옵션들로는

- `tableName`: 실제 데이터 베이스의 테이블 이름을 설정
- `paranoid`: 이 속성을 `true`로 설정하면 `deletedAt`이라는 커럼이 생긴다. 로우를 삭제하게 되면 실제 데이터는 삭제되지 않고 `deletedAt` 컬럼에 지운 시간이 기록된다. 그 후에 `SELECT`를 수행하면 해당 로우는 집계되지 않는다.
- `underscored`: 시퀄라이즈의 테이블명과 컬럼명은 기본값이 CalmelCase 이다. 이 옵션이 `true`이면 이름들이 SnakeCase로 바뀐다.

---

### 생성한 Model을 sequelize 객체에 연결하기

앞에는 모두 define() 메서드로 모델을 생성하는 내용이었고, 이제 생성한 모델을 sequelize 객체에 연결해야한다.

`Models/index.js`로 들어가서 코드 한 줄만 추가해주면 된다.

```javascript
// Models/index.js

const Sequelize = require('sequelize');
const env = process.env.NODE_ENV || 'development';
const config = require('../config/config.json')[env];
const db = {};

let sequelize;
if (config.use_env_variable) {
    sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
    sequelize = new Sequelize(config.database, config.username, config.password, config);
}
db.sequelize = sequelize;
db.Sequelize = Sequelize;

// !! 이렇게 User 모델을 추가하면 된다.
db.User = require('./user')(sequelize, Sequelize);

module.exports = db;
```

