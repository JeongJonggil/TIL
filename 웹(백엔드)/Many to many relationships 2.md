# Many to many relationships 2

### 1. 프로필

- 프로필 구현

@@@@@@@@@@@@[1]~[5]img@@@@@@@@@@@

### 2. 팔로우

- User(M) - User(N) 
- 회원은 0명 이상의 팔로워를 가질 수 있고, 0명 이상으 ㅣ다른 회원들을 팔로잉 할 수 있음
- 팔로우 구현

@@@@@@@@@@@@[6]~[]img@@@@@@@@@@@

### 3. .exists()

- QuerySet에 결과가 포함되어 있으면 True를 반환하고 결과가 포함되어 있지 않으면 False를 반환

- 큰 QuerySet에 있는 특정 객체 검색에 유용

  ```python
  #예시
  if person.follower.filter(pk=request.user.pk).exists():
  ```

  