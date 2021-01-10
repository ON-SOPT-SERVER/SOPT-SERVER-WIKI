## MySQL Workbench

### Index

1. [데이터베이스 세팅](#데이터베이스-세팅)
2. [스키마 생성](#스키마-생성)
3. [ERD 보기](#er-diagram-보기)

---

### 데이터베이스 세팅

우리는 RDS로 연습했으니까 그대로 씀.

1. 워크벤치 실행했을 때 보이는 홈화면에서 **`MySQL Connections` 옆에 있는 + 아이콘을 클릭한다**
2. 새 창이 뜨면,
   - `Connection Name`에는 워크벤치에서 보여지는 데이터베이스 이름을
   - `Parameters` > `Hostname` 에는 RDS 엔드포인트 주소를
   - `Username`에는 유저네임(admin)을
   - `Password`에는 비밀번호를 넣으면 된다.
3. `OK`를 누르고, 연결에 성공하면 **Successfully made the MySQL connection** 이라는 문구가 뜬다.
   - 만약에 **Fail**이 나오면 RDS 초기 설정시 **퍼블릭 엑세스 가능** 을 **'예'**로 해 놓았는지 확인해본다.
4. 마지막으로 `Test Connection`을 하고 마무리하면 된다.

---

### 스키마 생성

 먼저, RDS 랑 연결한 DB를 연다.

새로운 스키마를 생성하기 위해

1. 상단바에 원기둥에 + 붙어있는 아이콘 클릭

2. 스키마 이름 원하는걸로 쓰고,

   - Character Set: `utf8`
   - Collation: `utf8_unicode_ci` 

   로 설정하고 `Apply`를 누른다.

3. 그러면 새 창으로 SQL문이 뜨는데 그걸 `Apply`(실행)하면 우리가 원하는 대로 스키마가 생성된다. 끝!

---

### ER diagram 보기

1. 워크벤치의 `Databese` > `Reverse Engineer` 클릭
2. 원하는 DB가 연결된 Connection 을 선택
3. `Continue` 클릭
4. 원하는 스키마를 선택
5. `Import MySQL Table Objects`에 체크, 원하는 테이블 고르기 (다 볼거면 그냥 `Execute`)
6. `Execute` 👉🏻 `Continue` 👉🏻 `Close` 하면 ERD가 뜬다.