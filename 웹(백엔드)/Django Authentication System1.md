# Django Authentication System1

### 1. 개요

- 우리가 서버로부터 받은 페이지를 둘러볼 때 우리는 서버와 서로 연결되어 있는 상태가 아님

### 2. HTTP

- HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 규약, 웹(WWW)에서 이루어지는 모든 데이터 교환의 기초

- ##### 특징

  - ##### 비 연결 지향(connectionless)

    : 서버는 요청에 대한 응답을 보낸 후 연결을 끊음

  - ##### 무상태(stateless)

    : 연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나며 상태 정보가 유지되지 않음

### 3. 쿠키(Cookie) & 세션(Session)

#### : 서버와 클라이언트 간의 상태를 유지하기 위한 목적으로 사용됨. 정보가 저장되는 위치에 따라 쿠키(클라이언트)와 세션(서버)을 구분해서 생각하면 됨

#### 	(1) 쿠키

​		●  서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각

##### 		● 클라이언트 측에서 저장되는 작은 데이터 파일이며, 사용자 인증, 추적, 상태 유지 등에 사용되는 데이터 저장 방식

##### 		● 쿠키 사용 예시

![1](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004102044441.png)

##### 			● 쿠키 사용 원리

![2](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004102404388.png)

​			● 쿠키 사용 목적

​				- 세션관리 : 로그인, 아이디 자동완성, 공지 하루 안 보기, 팝업 체크, 장바구니 등의 정보 관리

​				- 개인화 : 사용자 선호, 테마 등의 설정

​				- 트레킹 : 사용자 행동을 기록 및 분석



#### 	(2) 세션(Session)

##### 		● 서버 측에서 생성되어 클라이언트와 서버 간의 상태를 유지하기 위해 상태 정보를 저장하는 데이터 저장 방식

​		● 쿠키에 세션 데이터를 저장하여 매 요청시마다 세션 데이터를 함께 보냄

​		● 세션 작동 원리

![3](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004103831862.png)

### 4. 쿠키(Cookie) & 세션(Session) 요약

- 

- #### **서버 측에서는 세션 데이터를 생성 후 저장하고 세션 ID를 생성, 해당 ID를 클라이언트 측으로 전달하여, 클라이언트는 쿠키에 이 ID를 저장**

- #### 서버로부터 쿠키를 받아 브라우저에 저장하고, 클라이언트가 같은 서버에 재요청 시마다 저장해 두었던 쿠키도 요청과 함께 전송

  > 예를 들어 로그인 상태 유지를 위해 로그인 되어 있다는 사실을 입증하는 데이터를 매 요청마다 계속해서 보내는것

- django에서는  세션을 저장하고 key를 발급하는 등 일련의 과정들을 내부적으로 처리해주기 때문에 우리가 구현할 필요는 없음. 우리는 결과를 이해하고 보기만 하면 됨

![4](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004105232647.png)

### 5. 인증(Authentication)

- 사용자가 자신이 누구인지 확인하는 것(신원 확인)

- auth와 관련한 경로나 키워드들을 django 내부적으로 accounts라는 이름으로 사용하고 있기 때문에 되도록 **앱 이름은 'accoutns'로 지정하는것을 권장**

### 6. Custom User Model

- django에서 기본적으로 제공하는 User model은 내장된 auth 앱의 User 클래스를 사용했었음. settings.py의 'django.contrib.auth'

- ##### 하지만, 개발자가 직접 User 정보에 대한 Field를 Custom 할 수 없는 문제가 존재하여 Custom User Model로 대체하여 사용.

- ##### Custom User Model 대체하기

  ![5](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004112049448.png)

![6](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004112106111.png)

![7](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004112124431.png)

- #### 주의사항

  ##### <span style="color:red"> ※ 주의 : 프로젝트 중간에 Auth_USER_MODEL을 변경 할 수 없음. </span>

  : 그래서 class User(AbstractUser): 를 pass로 선언해놓고 시작하는 거임. 미리 pass로라도 선언을 해놓고 진행하기 때문에 프로젝트 중간이라도 필드에 대한 수정이 가능함. 만약 Custom User Model 를 잊고 프로젝트가 이미 진행되고 있을 경우 데이터베이스 초기화 후 Custom User Model 생성 후 진행하면 됨

![8](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004113939814.png)

### 7. Login

- ##### Session을 Create하는 과정이 Login

- django에서는 로그인/회원가입/회원정보수정/비밀번호변경에 필요한 form이 built-in 되어 있음

- ##### 로그인 페이지 작성(create-view 함수와 거의 동일함)

![9](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004115914827.png)

- AuthenticationForm() : 로그인 인증에 사용할 데이터를 입력받는 built-in form
- get-user() : AuthenticationForm의 인스턴스 메서드
      → 유효성 검사를 통과했을 경우 로그인 한 사용자 객체를 반환

### 8. Logout

- ##### Session을 delete 하는 과정이 Logout

- logout(request) : 현재 요청에 대한 Session Data를 DB에서 삭제, 클라이언트의 쿠키에서도 Session Id를 삭제



### 9. Template with Authentication data

- ##### context processors : view함수에서 따로 context로 넘기지 않아도 settings.py-templates에 미리 load되어 호출이 가능한 변수들

![10](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20231004141941609.png)

### 10.  참고(Abstract base classes, 추상 기본 클래스)

##### - Abstract base classes, 추상 기본 클래스

- 다른 자식 클래스를 찍어내기 위한 클래스로, 자식 클래스를 찍어내기 위한 틀
- migrate를 해도 table이 만들어지지 않도록 설계되어 있으며, 대신 다른 모델의 기본 클래스로 사용되는 경우 해당 필드가 하위 클래스의 필드에 추가됨.
- 파이썬에서 보통 Abstract가 붙어있으면 추상 기본 클래스임