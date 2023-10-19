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

  
