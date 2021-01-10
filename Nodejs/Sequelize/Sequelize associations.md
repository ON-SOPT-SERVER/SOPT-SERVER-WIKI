## Sequelize associations

### 📌 Index

1. [Association](#association)
2. [1:1관계](#1:1-관계)
3. [1:M관계](1:m-관계)
4. [N:M관계](#n:m-관계)

---

### Association

: 시퀄라이즈에서 관계를 정의할 때 지원하는 **sequelize 모델**의 서브클래스(sub class)

시퀄라이즈는 다음 4가지의 Sub Class(Association)를 지원한다.

- `hasOne`
- `belongsTo`
- `belongsToMany`
- `hasMany`

우리는 **테이블의 Relation에 따라** 알맞은 Association을 사용해주면 된다🤩

세미나에서 Association을 만들어본 예제를 다시 봅시다

😊

Like, User, Post, Profile 테이블이  다음과 같이 있다.

> `User`: id, email, userName, password, salt
>
> `Post`: id, title, contents, postImageUrl, createdAt, updatedAt, UserId
>
> `Like`: UserId, PostId, createdAt, updatedAt



테이블 간 의 관계는

> User : Profile 👉🏻 1 : 1
>
> User : Like 👉🏻 1 : N
>
> User : Post 👉🏻 1 : N
>
> Post : Like 👉🏻 N : M

위와 같았다 😆 한 번 더 해보자.

---

### 1:1 관계

#### User - Profile 👉🏻 한 명의 사용자는 한 개의 Profile을 가진다.

> User has one profile.
>
> Profile belongs to user.

```javascript
db.User = require('./user')(sequelize, Sequelize);
db.Profile = require('./profile')(sequelize, Sequelize);

db.User.hasOne(db.Profile);
db.Profile.belongsTo(db.User);
```

🤔 hasOne과 belongsTo가 반대가 되면? **안 된다.**

👉🏻 `belongsTo`를 사용하는 Profile 모델에 User 구별 외래키가 생성되기 때문이다.

---

### 1:M 관계

#### User - Post 👉🏻 한 명의 사용자는 여러 개의 게시글을 작성할 수 있다.

> User has many posts.
>
> Post belongs to user.

```javascript
db.User = require('./user')(sequelize, Sequelize);
db.Post = require('./post')(sequelize, Sequelize);

db.User.hasMany(db.Post);
db.Post.belongsTo(db.User);
```

**만약 외래키 이름을 지정해주지 않으면,** 기본적으로

`hasMany`를 사용하는 테이블 이름+ Id 로 설정된다. 이 예제에서는 UserId 컬럼이 생기는 것이다.

#### 외래키에 옵션 추가하기

```javascript
db.User.hasMany(db.Post, { foreignKey: { name: 'UserId', allowNull: false }, onDelete: 'cascade' });
db.Post.belongsTo(db.User);
```

- `allowNull: false` 👉🏻 hasMany()에서 외래키에 옵션을 추가했다.  (Not Null)

  옵션을 추가하지 않는다면,

  ```javascript
  db.User.hasMany(db.Post, { foreignKey: 'UserId', onDelete: 'cascade' });
  ```

  이렇게 쓰면 된다.

- `onDelete: 'cascade'` 👉🏻만약 어떤 유저가 탈퇴를 해서 User 테이블에서 유저 데이터가 사라지면, 그 유저가 쓴 포스트들도 Post 테이블에서 삭제되게하는 옵션이다. 말 그대로 **외래키 테이블에 종속적으로 삭제된다**는 뜻이다.

  `onDelete`의 **Default**는 set Null이다.

- `onUpdate: 'cascade'` : Default

---

### M:N 관계

#### User - (Like) - Post 👉🏻 여러 명의 사용자가 여러 개의 게시글에 좋아요를 누를 수 있다.

> User belongs to many posts
>
> Post belongs to Many users

`On delete: cascade`, `On update: cascade` 가 기본값이다. 모두 종속!

```javascript
// Like 모델 정의

const { User, Post } = require('../models');

module.exports = (sequelize, DataTypes) => {
    return sequelize.define('Like', {
        PostId: {
            type: DataType.INTEGER,
            reference: {
                model: Post,
                key: 'id',
            },
        },
        UserId: {
            type: DataTypes.INTEGER,
            reference: {
                model: User,
                key: 'id',
            },
        },
    }, {
        freezeTableName: true,
        timeTables: ture,
    })
}
```

```javascript
// models/index.js

db.User = require('./user')(sequelize, Sequelize);
db.Post = require('./post')(sequelize, Sequelize);
db.Like = require('./like')(sequelize, Sequelize);

// Association 1
db.User.hasMany(db.Post, { onDelete: 'cascade' });
db.Post.belongsTo(db.User);

// Association 2
db.User.belongsToMany(db.Post, { through: 'Like', as: 'Liked' });
db.Post.belongsToMany(db.User, { through: 'Like', as: 'Liker' });
```
**주의 사항** ❗

`User` 모델은 `Post` 모델과 두 번의 Association 을 가지고 있다. 따라서 **두 Association에서** `User` 모델이 보는 `Post` 모델의 **이름이 중복되면 안된다**.

그래서 위의 코드를 보면 `as`를 사용해서 `User`의 별칭을 `Liked`로 지어준 것이다.
(`Post` -> `User`도 마찬가지, `User`의 별칭을 `Liker`로 설정한다.🤩)




