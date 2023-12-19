# 자바 스프링 프로젝트 Q&A(나중에 정리하기)

### 1. 1:N 관계와 역참조

- a : b 클래스가 1 : N 관계일 때,

- b 필드에 @ManyToOne필드를 작성(django의 ForeignKey와 유사)

- 추가로 역참조 구현 시 a 클래스에 @OneToMany어노테이션 작성 필요 (django는 모델 매니저를 통해 역참조를 이용가능했지만 스프링은 역참조 시 @OneToMany로 직접 명시해줘야 됨)

  ```java
  //ex
  
  @Entity
  public class Question {
      @OneToMany(mappedBy = "question", cascade = CascadeType.REMOVE)
      private List<Answer> answerList;
  }
  
  @Entity
  public class Answer {
      @ManyToOne
      private Question question;
  }
  ```

  

  > GPT : Java Spring에서는 이런 자동화된 역참조가 없습니다. `@OneToMany`와 `@ManyToOne` 어노테이션을 통해 명시적으로 양방향 관계를 설정해야 합니다. 



### 2. entity에 작성한 코드대로 DB에 테이블 생성 기능

- JPA (Java Persistence API)와 함께 Hibernate와 같은 ORM(Object-Relational Mapping) 툴을 사용하면, 엔티티(Entity) 클래스에 작성된 코드를 기반으로 MySQL 데이터베이스에 테이블을 자동으로 생성할 수 있습니다.

  - **DDL 자동 생성 설정 설정** : 데이터베이스 스키마를 자동으로 생성하도록 설정하기 위해, `application.properties` 파일에서 `spring.jpa.hibernate.ddl-auto` 속성을 설정해야 합니다. 이 속성은 다음과 같은 값으로 설정될 수 있습니다:
    - `create`: 기존 테이블을 삭제하고 매번 새로운 테이블을 생성합니다.
    - `update`: 데이터베이스 스키마를 현재 엔티티 구조에 맞게 업데이트합니다. 기존 데이터는 유지됩니다.
    - `create-drop`: 애플리케이션이 시작될 때 테이블을 생성하고, 종료될 때 테이블을 삭제합니다.
    - `validate`: 엔티티와 테이블이 정확히 매치되는지 검증만 합니다. 테이블을 생성하거나 수정하지 않습니다.
    - `none`: 자동 생성 기능을 사용하지 않습니다.

  ```properties
  spring.jpa.hibernate.ddl-auto= 속성명
  ```



### 3. @ResponseBody와 RestController

- `@ResponseBody` 
  - 반환 값(return)이 직접 응답 본문으로 전송되고, Spring의 메시지 변환기가 객체를 JSON 또는 XML로 자동으로 직렬화합니다.
  - `@controller`에 `@ResponseBody`가 적용이 안되어 있으면 기본적으로 return에서 view파일(html 등)을 찾게 됨. `@ResponseBody`를 적용하지 않을 시 기본적으로 문자열을 직렬화하여 return시켜 줌.  
- `@RestController`
  - `@Controller`와 `@ResponseBody`를 결합한 것. 클래스 내의 모든 메서드에 자동으로 `@ResponseBody`가 적용되어 모든 메서드의 반환값이 기본적으로 응답 본문으로 직접 전송됨.



### 4. 의존성 주입(DI)

- 생성자 주입

  - `@RequiredArgsConstructor` 어노테이션이 생성자 주입 방식
  - 아래 1번 코드의 `@RequiredArgsConstructor`을 통한 생성자 주입 로직은 2번 코드와 같음

  ```java
  // 1번
  @RequiredArgsConstructor
  @RestController
  public class QuestionController {
      private final QuestionRepository questionRepository;
  }
  ```

  ```java
  // 2번
  @RestController
  public class QuestionController {
      private final QuestionRepository questionRepository;
  
      // Lombok의 @RequiredArgsConstructor가 이와 같은 생성자를 자동으로 생성합니다
      public QuestionController(QuestionRepository questionRepository) {
          this.questionRepository = questionRepository;
      }
  
  }
  
  // QuestionController 클래스는 QuestionRepository 타입의 파라미터를 받는 생성자를 가지고 있습니다. Spring 컨테이너는 이 생성자를 사용하여, 자동으로 생성하거나 관리하고 있는 QuestionRepository의 인스턴스를 QuestionController에 주입합니다.
  ```

- 필드 주입

  ```java
  @Service
  public class MyService {
      @Autowired
      private MyRepository myRepository;
  }
  ```

  

- 수정자 주입

  ```java
  @Service
  public class MyService {
      private MyRepository myRepository;
  
      @Autowired
      public void setMyRepository(MyRepository myRepository) {
          this.myRepository = myRepository;
      }
  }
  ```




### 4. Auth(Spring Security 라이브러리)

- Spring Security 라이브러리로 로그인, 로그아웃 등 인증 및 권한 기능 구현 가능 
- 회원가입, 회원정보 수정 등 회원객체 데이터 생성에 관한 정보는 따로 구현해야 됨(Spring Security에 없음)
  - 아무래도 회원가입등 유저정보에 대한 User 객체는 커스텀 필드가 많이 생성될 수 있음.
  - 이 때 추가 필드가 생성되면 Spring Security를 사용하는 로직에 문제가 생길 가능성이 있어서 분리해 놓은듯?? -> 내 추측

- `@Configuration`에 보안 관련 설정, `@Service`에 로그인,로그아웃 관련 비지니스 로직 작성 해야됨
  - https://wikidocs.net/162255 참고
- entity의 클래스명을 User로 사용할 경우 Spring Security 라이브러리에 있는 User 클래스와 충돌 될 수 있음
  - Spring Security 라이브러리에 있는 User 클래스를 커스텀해서 사용하거나 (커스텀이 꼭 필요한게 아니면 그냥 클래스명을 구분지어서 쓰자)
  - 아니면 각 User 클래스를 사용할 때 패키지명까지 명시해서 두 개의 구분을 확실히 짓도록 하면 됨