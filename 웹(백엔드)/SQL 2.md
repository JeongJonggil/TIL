# SQL 2

### 1. DDL (Data Definition Language)

- 데이터의 기본 구조 및 형식 변경 (주로 필드와 연관)

**→ DDL은 테이블의 필드를 변경, DML은 레코드 수정 느낌**

- CREATE, DROP, ALTER 등

- 예시

  ```sqlite
  -- 테이블 생성(CREATE TABLE)
  -- '필드명-데이터타입-제약조건-추가옵션 키워드' 순으로 작성
      CREATE TABLE examples (
          ExamID INTEGER PRIMARY KEY AUTOINCREMENT, --ATUONINCREMENT : 자동 증가
          LastName VARCHAR(50) NOT NULL,
          FirstName VARCHAR(50) NOT NULL
      );
  
  -- 테이블 구조에 관한 정보 확인(Sqlite3)
  -- cid --> 컬럼 아이디
  PRAGMA table_info('examples');
  
  
  -- 테이블 구조 변경(ALTER TABLE)
      -- 필드 추가
      -- sqlite는 ADD COLUMN에 여러개 컬럼 넣기 안됨
      ALTER TABLE
          examples
      ADD COLUMN
          Country VARCHAR(50) NOT NULL DEFAULT 1;
          
      ALTER TABLE
          examples
      ADD COLUMN
          Age INTEGER NOT NULL DEFAULT 1;
          
      ALTER TABLE
          examples
      ADD COLUMN
          Address VARCHAR(50) NOT NULL DEFAULT 1;
  
      -- 필드명 변경
      ALTER TABLE
          examples
      RENAME COLUMN
          Address TO PostCode;
      
      -- 필드 삭제 (SQLite 버전에 따라 DROP COLUMN 직접 사용 불가능 함) -> 그냥 버전 업 시켜서 필드 삭제만 가능한 버전을 사용하기
  		-- 그게 아니면 삭제할 필드를 제외한 새로운 복제 테이블 생성 후 기존 테이블을 지우는 방식으로 사용해야함
      -- SQLite에서 CREATE TABLE ... AS SELECT ... 문을 사용하면, 새로 생성된 테이블은 원본 테이블의 데이터는 가지고 오지만, 원본 테이블의 여러 속성과 제약 조건(예: PRIMARY KEY, UNIQUE, NOT NULL 등)은 상속받지 않음.
      -- SQLite에서는 제약 조건이나 인덱스를 포함하여 구조를 그대로 복사하는 내장 기능이 없어서 테이블에 이러한 제약조건을 적용하려면, 처음에 테이블을 생성할 때 명시적으로 이러한 제약조건을 지정해주어야 함 
      -- 결론은 CREATE TABLE... AS SELECT ...로 복제하면 안되고 CREATE TABLE로 필드명, 속성,제약사항 동일하게 하나씩 다 만들어서 데이터만 복제시켜야됨 -> 굉장히 비효율적
          -- examples의 Country 필드 삭제
              ALTER TABLE
                  examples
              DROP COLUMN
                  Country;
  
  		-- 테이블 삭제
  			DROP TABLE examples;
  ```

  

※ 주의 ※ 

> SQLite은 테이블이 이미 만들어진 후에는 제약조건을 수정할 수 없다. 만약 데이터를 보존하면서 테이블에 제약조건만 바꾸고 싶은 경우에는 새 테이블을 만들어서 데이터를 복사한 후 이전 테이블을 삭제하는 방법을 사용해야 함
>
> 1. 기존 테이블 스키마에서 제약조건을 포함한 새로운 스키마를 이용해 새 테이블을 만든다. 
>
>  \- 기존 테이블[example] 스키마
>
> ```sql
> CREATE TABLE example(
>     id varchar(12)
>     name varchar(12),
>     age varchar(2)
> );
> ```
>
>  \- 새 테이블[new_example] 스키마
>
> ```sql
> CREATE TABLE new_example(
>     id varchar(12)
>     name varchar(12),
>     age varchar(2),
>     PRIMARY KEY(id)
> );
> ```
>
> 2. 기존 테이블에서 새 테이블로 모든 데이터를 복사한다.
>
> ```sql
> INSERT INTO new_example SELECT * FROM example;
> ```
>
> 3. 기존 테이블을 삭제한다.
>
> ```sql
> DROP TABLE example;
> ```
>
> 4. 새 테이블의 이름을 기존 테이블의 이름으로 바꾼다.
>
> ```sqlite
> ALTER TABLE new_example RENAME TO example;
> ```



### 2. 타입 선호도(참고)

[1]~[2] 이미지 업로드



### 3. DML(Data Manipulation Language)

- 데이터 조작(레코드 추가,수정,삭제)

  **→ DDL은 테이블의 구조를 변경, DML은 레코드 수정 느낌**

- INSERT, UPDATE, DELETE 등

- **실무에서는 데이터를 잘 지우지 않기 때문에 DB에서의 문제는 데이터를 수정하는 과정에서 많이 발생함**

- 예시

  ```sqlite
  -- INSERT INTO (레코드 입력) 
      -- TABLE 생성
      CREATE TABLE articles (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      title VARCHAR(100) NOT NULL,
      content VARCHAR(200) NOT NULL,
      createdAt DATE NOT NULL
      );
  
      --TABLE 구조 확인
      PRAGMA table_info('articles');
  
      -- DATA 입력
      INSERT INTO
          articles(title,content, createdAT)
      VALUES
          ('title1','content1','2023-10-10'),
          ('title2','content2','2023-10-11'),
          ('title3','content3','2023-10-12');
  
      -- DATA 입력
      INSERT INTO
          articles(title,content, createdAT)
      VALUES
          ('title4','content4',DATE());
  
  
  -- UPDATE ... SET (레코드 수정)
      --4번 id를 기준으로 title, content수정 하고 id 기준 내림차순 조회
      UPDATE
          articles
      SET
          title = 'update TITLE',
          content = 'update content'
      WHERE
          id = 4;
  
      SELECT
          *
      FROM
          articles
      ORDER BY
          id DESC;
  
  -- DELETE FROM .. [WHERE condition](레코드 삭제)
      DELETE FROM albums
      WHERE AlbumID =5;
  
      -- articles에서 created가 가장 오래된 2개 레코드 지우기
      DELETE FROM articles
      WHERE createdAT IN (SELECT createdAT FROM articles ORDER BY createdAT
      LIMIT 2);
  ```