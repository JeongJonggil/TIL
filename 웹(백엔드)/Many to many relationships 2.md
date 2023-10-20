# Many to many relationships 2

### 1. 프로필

- 프로필 구현

![1](https://github.com/JeongJonggil/TIL/assets/139416006/48d363b2-c85c-42f1-a8c6-77c66dfb5289)
![2](https://github.com/JeongJonggil/TIL/assets/139416006/5d370a2e-5046-438e-a227-f4ee4db61191)
![3](https://github.com/JeongJonggil/TIL/assets/139416006/cfb8b5c3-802d-45fd-8c97-9afdd7a5c0d0)
![4](https://github.com/JeongJonggil/TIL/assets/139416006/4bff2304-ca6b-4619-83e7-db64d60c5f3f)
![5](https://github.com/JeongJonggil/TIL/assets/139416006/439b21fe-2881-4f1e-8584-812048e6d4e8)


### 2. 팔로우

- User(M) - User(N) 
- 회원은 0명 이상의 팔로워를 가질 수 있고, 0명 이상으 ㅣ다른 회원들을 팔로잉 할 수 있음
- 팔로우 구현

![6](https://github.com/JeongJonggil/TIL/assets/139416006/8219885c-c904-45b5-b66e-f8644187b4d9)
![7](https://github.com/JeongJonggil/TIL/assets/139416006/5a86bb51-c500-47c8-9bc9-9c8d905c2ccd)
![8](https://github.com/JeongJonggil/TIL/assets/139416006/1b1f890b-6af0-4b64-8faf-128259a1ba1f)
![9](https://github.com/JeongJonggil/TIL/assets/139416006/8621aecf-3f82-4053-9350-87c8cc0d7567)
![10](https://github.com/JeongJonggil/TIL/assets/139416006/56342d1f-1cb9-4613-94f0-5ef17cabd918)
![11](https://github.com/JeongJonggil/TIL/assets/139416006/00519186-24ed-4b3c-b4e1-caecda2be544)


### 3. .exists()

- QuerySet에 결과가 포함되어 있으면 True를 반환하고 결과가 포함되어 있지 않으면 False를 반환

- 큰 QuerySet에 있는 특정 객체 검색에 유용

  ```python
  #예시
  if person.follower.filter(pk=request.user.pk).exists():
  ```




### 4. Fixtures

- Django가 데이터베이스로 가져오는 방법을 알고 있는 데이터 모음
- 데이터베이스 구조에 맞추어 작성 되어 있음
- 초기데이터 제공에 사용됨

@@@@@@@@@@@@@@@@@@@@[1]@@@@@@@@@@@@@@@

- fixtures 관련 명령어

  (1) dumpdata : 생성 (데이터 추출) 

   - 데이터베이스의 모든 데이터를 추출
   - 추출한 데이터는 json 형식으로 저장'
   - **json파일은 직접 만들지 말 것(dumpdata 사용하기)**

  ```python
  #작성 예시
  
  $ python manage.py dumpdata [app_name[.ModelName] [app_name[.ModelName] ...]] > filename.json
  
  #ex1 기본예제
  $ python manage.py dumpdata --indent 4 articles.article > articles.json
  #--indent 4 는 json데이터를 가독성 좋게 하기 위해 들여쓰기 4칸을 해서 json파일을 작성하겠다는 의미
  
  #ex2 3개의 모델을 하나의 json 파일로 
  $ python manage.py dumpdata --indent 4 articles.article articles.comment accounts.user> data.json
  
  #ex3 모든 모델을 하나의 json 파일로 
  $ python manage.py dumpdata --indent 4 > data.json
  ```

  

  (2) loaddata : 로드 (데이터 입력)

  - Fixtures 데이터를 데이터베이스로 불러오기
  - fixtures 파일 기본 경로 : app_name/fixtures/
  - Django는 설치된 모든 app의 디렉토리에서 fixtures 폴더 이후의 경로로 fixtures 파일을 찾아 load

  ```python
  #작성 예시
  $ python manage.py loaddata articles.json users.json comments.json
  ```

- **loaddata 관련 에러/주의사항**

  - loaddata 시 encoding codec 관련 에러가 발생하는경우

    (1) dumpdata 시 추가 옵션 작성

    ```python
    $ python -Xutf8 manage.py dumpdata [생략]
    ```

    (2) 메모장 활용

    - 메모장으로 json 파일 열기
    - "다른 이름으로 저장" 클릭
    - 인코딩을 UTF8로 선택 후 저장

  - **loaddata 순서 주의사항 : loaddat를 한방에 할 때는 장고가 알아서 순서 맞춰줘서 상관 없음**

@@@@@@@@@@@@@@@@@@@@[2]@@@@@@@@@@@@@@@

### 4. Improve query(쿼리 개선)

- 같은 결과를 얻기 위해 DB측에 보내는 쿼리 개수를 점차  줄여 조회하기

  (1) annotate 사용

  - SQL의 GROUP BY 쿼리를 사용
  - @@@@@@@@@@@@@@@@@@@@[3]~[6]@@@@@@@@@@@@@@@

  

  (2) select_related

  - SQL의 INNER JOIN 쿼리를 활용
  - 1:1 또는 N:1참조 관계에서 사용
  - @@@@@@@@@@@@@@@@@@@@[7]~[10]@@@@@@@@@@@@@@@

  

  (3) prefetch_related

  - M:N 또는 N:1 역참조 관계에서 사용
  - SQL이 아닌 Python을 사용한 JOIN을 진행
  - @@@@@@@@@@@@@@@@@@@@[11]~[14]@@@@@@@@@@@@@@@

  ​	

