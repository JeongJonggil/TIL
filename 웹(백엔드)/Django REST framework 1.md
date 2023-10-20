# Django REST framework 1

### 1. REST API

- API(Application Programming Interface) 
  - 애플리케이션과 프로그래밍으로 소통하는 방법
  - 클라이언트-서버처럼 서로 다른 프로그램에서 요청과 응답을 받을 수 있도록 만든 체계

- REST(Representational State Transfer)

  - API Server를 개발하기 위한 일종의 소프트웨어 설계 방법론 "약속(규칙X)"

  - REST 원리를 따르는 시스템을 RESTful 하다고 부름

  - **"자원을 정의"**하고 **"자원에 대한 주소를 지정"**하는 전반적인 방법을 서술

    > "각각 API구조를 작성하는 모습이 너무 다르니 약속을 만들어서 다같이 통일해서 쓰자!"

- REST API
  - REST라는 설계 디자인 약속을 지켜 구현한 API

![1](https://github.com/JeongJonggil/TIL/assets/139416006/8d668953-f1ee-41c4-b530-ac565566bcc5)




### 2. 자원의 식별

- URI(Uniform Resource Identifier, 통합 자원 식별자)

  - 인터넷에서 리소스(자원)를 식별하는 문자열
  - 가장 일반적인 URI는 웹 주소로 알려진 URL (URL보다 조금 더 큰 범주를 나타내는 개념)

- URL(uniform Resource Locator, 통합 자원 위치)

  - 웹에서 주어진 리소스의 주소

  - 네트워크 상에 리소스가 어디 있는지를 알려주기 위한 약속

![2](https://github.com/JeongJonggil/TIL/assets/139416006/15ca4a78-1a98-43b1-a41b-158a22a7dd07)


  - > 1. Schema (or Protocol)
    >    - 브라우저가 리소스를 요청하는데 사용해야 하는 규약
    >    - URL의 첫 부분은 브라우저가 어떤 규악을 사용하는지를 나타냄
    >    - 기본적으로 웹은 HTTP(S)를 요구하며 메일을 열기위한 mailto:, 파일을 전송하기 위한 ftp: 등 다른 프로토콜도 존재
    >
    > 2. Domain Name
    >    - 요청 중인 웹 서버를 나타냄
    >    - 어떤 웹 서버가 요구되는 지를 가리키며 직접 IP 주소를 사용하는 것도 가능하지만, 사람이 외우기 어렵기 때문에 주로 Domain Name으로 사용
    >    - 예를 들어 도메인 google.com의 IP 주소는 142.251.42.142
    > 3. Port
    >    - 웹 서버의 리소스에 접근하는데 사용되는 기술적인 문(Gate)
    >    - HTTP 프로토콜의 포준 포트
    >    - 표준 포트만 생략 가능
    > 4. Path
