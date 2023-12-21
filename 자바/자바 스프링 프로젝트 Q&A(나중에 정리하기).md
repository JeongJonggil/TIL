# 자바 스프링 프로젝트 Q&A(나중에 정리하기)

## ▣ 에러 모음

1. **java.lang.IllegalArgumentException:** Name for argument of type [java.lang.Integer] not specified, and parameter name information not found in class file either.

   - @PathVariable 사용시 name옵션으로 url의 변수 이름을 명시 안해두면 못찾을 수도 잇음

   - 아래 (name="id") 설정하니까 해결됨

     - ```java
       @PutMapping("/question/update/{id}")
       public ResponseEntity<Question> updateQuestion(@PathVariable(name="id") Integer id,   @ModelAttribute @Valid QuestionDto questionDto) {}
       ```

<hr>

### ▣ 내용 

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

  - https://wikidocs.net/162255 
  - https://samori.tistory.com/64 

- entity의 클래스명을 User로 사용할 경우 Spring Security 라이브러리에 있는 User 클래스와 충돌 될 수 있음
  - Spring Security 라이브러리에 있는 User 클래스를 커스텀해서 사용하거나 (커스텀이 꼭 필요한게 아니면 그냥 클래스명을 구분지어서 쓰자)
  - 아니면 각 User 클래스를 사용할 때 패키지명까지 명시해서 두 개의 구분을 확실히 짓도록 하면 됨

- **`SecurityConfig`** 예시 코드

  ```java
  package com.ssafy.finalpjt.user.config;
  
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  import org.springframework.http.HttpMethod;
  import org.springframework.security.authentication.AuthenticationManager;
  import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
  import org.springframework.security.config.annotation.web.builders.HttpSecurity;
  import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
  import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
  import org.springframework.security.crypto.password.PasswordEncoder;
  import org.springframework.security.web.SecurityFilterChain;
  import org.springframework.security.web.header.writers.frameoptions.XFrameOptionsHeaderWriter;
  import org.springframework.security.web.util.matcher.AntPathRequestMatcher;
  
  @Configuration
  @EnableWebSecurity
  public class SecurityConfig {
      @Bean
      SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
          http
                  .authorizeHttpRequests((authorize) -> authorize
                          .requestMatchers("/**").permitAll() // 인증이 필요없는 url 설정 : 모든 url에 대해 인증이 필요 없도록 해놨음(POSTMAN으로 동작 실험하기 위해)
                          .anyRequest().authenticated()) // 그 외의 url은 모두 인증이 필요함
                  .csrf().disable() // CSRF 보호 비활성화(POSTMAN으로 동작 실험하기 위해)
  //                //원래 csrf 관련 코드
  //                .csrf((csrf) -> csrf
  //                        .ignoringRequestMatchers(new AntPathRequestMatcher("/"))) csrf 인증 예외시킬 url주소
  
                  .headers((headers) -> headers
                          .addHeaderWriter(new XFrameOptionsHeaderWriter(
                                  XFrameOptionsHeaderWriter.XFrameOptionsMode.SAMEORIGIN)))
                  .formLogin((formLogin) -> formLogin
                          .loginPage("/user/login")
                          .defaultSuccessUrl("/"))
                  .logout((logout) -> logout
                          .logoutRequestMatcher(new AntPathRequestMatcher("/user/logout"))
                          .logoutSuccessUrl("/")
                          .invalidateHttpSession(true))
          ;
          return http.build();
      }
  
      @Bean
      AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception {
          return authenticationConfiguration.getAuthenticationManager();
      }
  
      @Bean
      PasswordEncoder passwordEncoder() {
          return new BCryptPasswordEncoder();
      }
  }
  ```

  



### 5. 디버깅 로그 활성화 하기

- 일반적으로 로그창에 나오는 에러 메시지들은 내용이 포괄적임 

- 더 자세한 에러메시지를 확인하고 싶으면, 에러가난 기능들의 디버깅 로그를 활성화 해야됨 (로그에 그냥 상세하게 메시지가 출력됨)

- 예를 들어 Spring security 라이브러리에서 계속 에러가 나는걸로 추정이 되어  `application.properties`에 하기 코드를 작성하고 url 요청을 하면 로그창에 자세한 에러메시지가 나옴

  ``` properties
  # Spring Security 라이브러리 정상동작 안해서 디버그 로그 활성화 하는 코드
  logging.level.org.springframework.security=DEBUG
  ```



### 6. csrf 토큰

- https://codevang.tistory.com/282 참고



### 7. @RequestBody

- request HTTP 요청의 본문(body)을 Java 객체로 변환하기 위해 사용. 클라이언트로부터 받은 JSON, XML 또는 기타 형식의 데이터를 컨트롤러 메서드의 매개변수에 매핑하는 데 사용

- @RequestBody를 사용하면 클라이언트 쪽에서 Json 타입으로 데이터가 넘어와야 함

- POSTMAN의 form-data 형식으로 받으려면 @ModelAttribute 어노테이션 사용

  ```java
  public ResponseEntity<Question> createQuestion(@ModelAttribute @Valid QuestionDto questionDto){}
  ```



