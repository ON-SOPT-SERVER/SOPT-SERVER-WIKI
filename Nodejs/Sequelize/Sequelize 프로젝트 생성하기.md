## Sequelize 프로젝트 생성하기

```bash
$ express [프로젝트 이름]
$ cd [프로젝트 이름]
$ npm install
```

여기까지는 기존에 했던 거랑 똑같다 !

이 프로젝트에서 sequelize를 사용하기 위해서 다음 3개의 모듈을 설치해야 한다.

```bash
$ npm install sequelize-cli sequelize mysql2
```

모듈이 모두 설치가 되면 다음 명령을 실행시켜 **시퀄라이즈 프로젝트**로 만들어 준다.

```bash
$ sequelize init
```

시퀄라이즈 프로젝트가 되면 다음 4개의 파일이 생성된다.

- config/config.json
- migrations/
- models/index.js
- seeders/

#### config/config.json

데이터베이스의 정보를 담는 공간이다. `development`, `test`, `production` 이렇게 3가지 배포 환경에 따라 각각 정의하고 사용할 수 있다. (세미나에서는 개발환경에 대해서만 다룸)

이 파일에서 각 객체의 **멤버 변수들을 사용하려는 DB에 맞게 수정**해줘야 한다.

```json
{
  "development": {
    "username": "root", // 유저 이름
    "password": null, // 연결하려는 DB 비밀번호
    "database": "database_development", //스키마 이름
    "host": "127.0.0.1", // DB의 IP 주소
    "dialect": "mysql"
  },
  "test": {
    ...
  },
  "production": {
    ...
  }
}

```

#### models/index.js

데이터베이스의 테이블을 정의하는 곳이다. 실제 우리가 사용할 MySQL 테이블과 프로젝트 내 시퀄라이즈의 모델은 대응된다!

#### Migrations

테이블 컬럼을 추가/제거할 때 migration 파일을 통해서 실제 DB에 반영한다. migration 파일을 통해 롤백도 가능하다.

#### Seeders

시드 데이터를 생성하는 곳, 주로 테스트 환경에서 샘플 데이터를 생성하고 지울 때 사용한다. 