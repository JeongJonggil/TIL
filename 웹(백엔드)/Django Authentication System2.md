# Django Authentication System2

### 1. 회원가입

- User 객체를 Create 하는 과정

- UserCreationForm() : 회원 가입시 사용자 입력 데이터를 받을 built-in ModelForm

  ![1](C:\Users\SSAFY\Desktop\images\Django Authentication System2\1.PNG)

![2](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005090624692.png)

![3](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005092820742.png)

![4](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005092900566.png)

![5](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005092926375.png)

![6](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005093210557.png)

![7](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005093234084.png)

> User 모델을 직접 참조하게 되면 User모델에 변경사항이 생겼을 떄 해당 모델을 참조하고 있는 부분들을 모두 직접 수정해야 됨. get_user_model() 을 통해 간접적으로 모델을 참조함으로써 모델에 수정사항이 생겼을때 이를 참조하고 있는 부분들을 수정해야하는 불편함이 줄어듬



### 2. 회원 탈퇴

- User 객체를 Delete 하는 과정

![8](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005093902185.png)

### 3. 회원정보 수정

- User 객체를 Update 하는 과정
- UserChangeForm() : 회원정보 수정 시 사용자 입력 데이터를 받을 built-in ModelForm

![9](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005100640362.png)

![10](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005100746789.png)

![11](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005100923657.png)

![12](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005101035283.png)

![13](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005101302867.png)



### 4. 비밀번호 변경

- 인증된 사용자의 Session 데이터를 Update 하는 과정
- PasswordChangeForm() : 비밀번호 변경 시 사용자 입력 데이터를 받을 built-in Form

![14](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231005102239577.png)

![15](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005103306078.png)

![16](C:\Users\SSAFY\Desktop\images\Django Authentication System2\16.PNG)

![17](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005103854924.png)

![18](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005104032215.png)

![19](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005104141475.png)

### 5. 인증된 사용자에 대한 접근 제한

- 로그인 사용자에 대해 접근을 제한하는 2가지 방법

  (1) is_authenticated 속성 

  : 사용자가 인증 되었는지 여부를 알 수 있는 User model의 속성.모든 User 인스턴스에 대해 항상 True인 읽기 전용 속성이며, 비인증 사용자에 대해서는 항상 False

  (2) login_required 데코레이터

  : 인증된 사용자에 대해서만 view 함수를 실행시키는 데코레이터. 비인증 사용자의 경우 /accounts/login/ 주소로 redirect 시킴

- #### is_authenticated 적용하기

![20](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005104833021.png)

![21](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005104900915.png)

- ##### login_required 적용하기

- ##### ![22](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005105436091.png)

![23](C:\Users\SSAFY\Desktop\images\Django Authentication System2\image-20231005105458960.png)