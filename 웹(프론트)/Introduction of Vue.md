# Introduction of Vue

### 1. Front-end Development

- 웹사이트와 웹 애플리케이션의 사용자 인터페이스 (UI)와 사용자 경험(UX)을 만들고 디자인하는 것
- HTML, CSS, JavaScript 등을 활용하여 사용자가 직접 상호작용하는 부분을 개발

### 2. Client-side frameworks

- 클라이언트 측에서 UI와 상호작용을 개발하기 위해 사용되는 자바스크립트 기반 프레임워크

- Client-side frameworks가 필요한 이유 

  - 웹에서 하는일이 많아졌다

    - 단순히 무언가를 읽는곳 → 무언가를 하는 곳

      @@@@@@@@@@@@@@ [1]

    - 다루는 데이터가 많아졌다

​			@@@@@@@@@@@@@@[2]

### 3. SPA(Single Page Application)

- 페이지 한 개로 구성된 웹 애플리케이션
- 웹 애플리케이션의 초기 로딩 후 새로운 페이지 요청 없이 동적으로 화면을 갱신하며 사용자와 상호작용하는 웹 애플리케이션 → CSR 방식

 	@@@@@@@@@@@@@@[2]

### 4. Client-side Rendering(CSR)

- 클라이언트에서 화면을 렌더링 하는 방식

- CSR 방식
  - 브라우저는 페이지에 필요한 최소한의 HTML 페이지와 자바스크립트를 다운로드
  - 그런 다음 자바스크립트를 사용하여 DOM을 업데이트하고 페이지를 렌더링
-  장점
  - 일반적으로 동일한 웹사이트의 다른 페이지로 이동하는 것이 **더 빠름**
  - 새로고침이 발생하지 않아 네이티브 앱과 유사한 **사용자 경험을 제공**
  - **Front-end와 Back-end의 명확한 분리**
    - Front-end는 UI 렌더링 및 사용자 상호 작용 처리를 담당 & Back-end는 데이터 및 API 제공을 담당

- 단점
  - 초기 구동속도가 느림
  - SEO(검색 엔진 최적화) 문제

### 5. Vue

- 개요
  - 사용자 인터페이스를 구축하기 위한 자바스크립트 프레임워크
  - 2023년 기준 최신 버전은 "Vue 3" → Vue 2 문서에 접속하지 않도록 주의
- Vue를 학습하는 이유
  - 새로운 개발자들도 빠르게 학습할 수 있음 (쉬운 학습 곡선 및 간편한 문법)
  - 반응성 시스템 (데이터 변경에 따라 자동으로 화면이 업데이트되는 기능을 제공)
  - 모듈화 및 유연한 구조
    - 애플리케이션을 컴포넌트 조각으로 나눌 수 있음
    - 코드의 재사용성을 높이고 유지보수를 용이하게 함

- Vue의 2가지 핵심기능
  - 선언적 렌더링 (Declarative Rendering)
    - HTML을 확장하는 템플릿 구문을 사용하여 HTML이 자바스크립트 데이터를 기반으로 어떻게 보이는지 설명할 수 있음
  - 반응형 (Reactivity)
    - 자바스크립트 상태 변경사항을 자동으로 추적하고 변경사항이 발생할 때 DOM을 효율적으로 업데이트

- 예시 코드

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <div id = "app">
    <h1>{{gretting}}</h1>
    <button @click="count++">{{ count }}</button>
    <p>{{ count }}</p>
    <h3>{{ count }}</h3>
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <script>
    const { createApp,ref } = Vue

    const app = createApp({
      setup(){
        const count = ref(0)
        const gretting = ref('hello')
        return {
          count,
          gretting
        }
      }
    })
    app.mount('#app')
  </script>
</body>

</html>
```

- Vue 사용법
  - Createapp 사용시 주의점 3가지
    - 인자로 객체를 받음
    - 인스턴스의 초기 상태와 로직은 setup()함수 안에 적어야 됨
    - template에서 값을 사용하려면 setup함수의 return 값으로 명시해야됨 (객체 타입으로 return문 작성)
  - ref는 반응형 변수를 만들기 위해 사용하는 것 \
  - 일단 기본적으로 변수는 const x = ref(인자) 형태로 생성하는게 좋음
    => **ref가 객체이기 때문에 const로 변수명을 선언해도 값을 바꾸는 것은 객체의 속성값을 바꾸는 거기 때문에 반응형으로 구현이 가능함**
  - v- on : click 는 @click 으로 작성 가능 

@@@@@@@@@@@@@@[4]-[13]



- 참고

@@@@@@@@@@@@[14]~[19]