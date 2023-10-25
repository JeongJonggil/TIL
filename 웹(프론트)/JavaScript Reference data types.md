# JavaScript Reference data types

### 1. 함수

- Function : 참조 자료형에 속하며 모든 함수는 function object

- 함수 구조

  - return값이 없다면 undefined를 반환

  ```javascript
  function name([param[,param[,...]]]){
  	return value
  }
  ```

- 함수 정의 2가지 방법

  - 선언식(function declartion)

    ```javascript
    function funcName(){
    	statements
    }
    
    //예시
    function add(num1,num2){
        return num1+num2
    }
    
    add(1,2) // 3
    ```

  - **표현식(function expression)**

    ```javascript
    const funcName = function(){
    	statements
    }
    
    //예시
    const sub = function(num1.num2){
        return num1 - num2
    }
    
    sub(2,1) // 1
    ```

- 함수 **표현식** 특징

  - 함수 이름이 없는 '익명 함수'를 사용할 수 있음

  - **선언식과 달리 표현식으로 정의한 함수는 호이스팅 되지 않으므로 함수를 정의하기 전에 먼저 사용할 수 없음**

  - 함수 선언식과 표현식 종합

    |      |                    선언식                    |                  표현식                  |
    | :--: | :------------------------------------------: | :--------------------------------------: |
    | 특징 | - 익명 함수 사용 불가능<br />- 호이스팅 있음 | - 익명함수 사용가능<br />- 호이스팅 없음 |
    | 기타 |                                              |              **사용 권장**               |



### 2. 매개변수

- 매개변수 정의 방법

  - 기본 함수 매개변수(Default function parameter)
    - 값이 없거나 undefined가 전달될 경우 이름 붙은 매개변수를 기본값으로 초기화

  ```javascript
  const greeting = function (name = 'Anonymous'){
  	return 'Hi ${name}'
  }
  
  greeting() // Hi Anonymous
  ```

  - 나머지 매개변수(Rest parameters)
    - 임의의 수의 인자를 '배열'로 허용하여 가변 인자를 나타내는 방법
    - 작성규칙
      - 함수 정의 시 나머지 매개변수 하나만 작성할 수 있음
      - 나머지 매개변수는 함수 정의에서 매개변수 마지막에 위치해야 함

  ```javascript
  const myFunc = function(param1, param2, ../ restParams){
  	return [param1, param2, restParams]
  }
  
  myFunc(1,2,3,4,5) // [1,2,[3,4,5]]
  myFunc(1,2)//[1,2,[]]
  ```

  - 매개변수와 인자의 개수 불일치 
    - **매개변수 개수 > 인자 개수 : 누락된 인자는 undefined로 할당**

  ```javascript
  const threeArgs = function(param1, param2, param3){
  	return [param1, param2, param3]
  }
  threeArgs() // [undefined,undefined,undefined]
  threeArgs(1) // [1, undefined, undefined]
  threeArgs(2,3) // [2,3,undefined]
  
  ```

  - 매개변수와 인자의 개수 불일치 
    - **매개변수 개수 < 인자 개수 : 초과 입력한 인자는 사용하지 않음**

  ```
  const noArgs = function (){
  	return 0
  }
  noArgs(1, 2, 3) // 0
  
  const twoArgs = function (param1,param2){
  	return [param1, param2]
  }
  twoArgs(1,2,3) // [1,2]
  ```



### 3. Spread syntax(전개 구문, '...')

@@@@@@@@@@@@@@@@@[1]~[3]



### 4. 화살표 함수(Arrow function expressions)

- 함수 표현식의 간결한 표현법

​	@@@@@@@@@@@@@@@@@[4]~[7]

- 참고

​	@@@@@@@@@@@@@@@@@[8]



### 5. 객체(object)

- 키로 구분된 데이터 집합(data collection)을 저장하는 자료형

​	@@@@@@@@@@@@@@@@@[9]~[12]



### 6. 객체와 함수

- Method
  - 객체 속성에 정의된 함수
  - object.method() 방식으로 호출
  - 메서드는 객체를 '행동'할 수 있게 함
  - 'this'키워드를 사용해 객체에 대한 특정한 작업을 수행 할 수 있음

- 'this' keyword
  - 함수나 메서드를 호출한 객체를 가리키는 키워드
    - 함수 내에서 객체의 속성 및 메서드에 접근하기 위해 사용

​	@@@@@@@@@@@@@@@@@[13]~[17], [35]@@@@@@@@@@@@@@@



### 7. 추가 객체 문법

- 단축 속성

​	@@@@@@@@@@@@@@@@@[18]

- 단축 메서드

​	@@@@@@@@@@@@@@@@@[19]

- 계산된 속성

​	@@@@@@@@@@@@@@@@@[20]~[22]

- Object with '전개 구문'

​	@@@@@@@@@@@@@@@@@[23]

- 유용한 객체 메서드

  @@@@@@@@@@@@@@@@@[24]

- Optional chaining('?.')

​	@@@@@@@@@@@@@@@@[25]~[29]

### 8. JSON

​	@@@@@@@@@@@@@@@@[30]~[31]

### 9. 배열(Array)

- 개요

  - Object(객체) : 키로 구분된 데이터 집합(data collection)을 저장하는 자료형 , **순서가 없음**

  - **Array(배열) : 순서가 있는** 데이터 집합을 저장하는 자료구조
    - 배열 요소 자료형 : 제약 없음
    - length 속성 사용 가능

- 메서드

  - |     메서드      |                      역할                      |
    | :-------------: | :--------------------------------------------: |
    |   push / pop    | 배열 끝 요소를 추가 / 제거(제거한 요소를 반환) |
    | unshift / shift | 배열 앞 요소를 추가 / 제거(제거한 요소를 반환) |

- Array Helper Methods

  - 배열을 **순회**하며 **특정 로직을 수행**하는 메서드

  - 메서드 호출 시 인자로 함수를 받는 것이 특징

  - | 메서드  | 역할                                                         |
    | ------- | ------------------------------------------------------------ |
    | forEach | 인자로 주어진 함수(콜백함수)를 배열 요소 각각에 대해 실행    |
    | map     | 배열 내의 모든 요소 각각에 대해 함수(콜백함수)를 호출하고, <br/>함수 호출 결과를 모아 **새로운 배열**을 반환 |

    ​	@@@@@@@@@@@@@@@@[36]~[45]

- 콜백함수(Callback function)

  - 다른 함수에 인자로 전달되는 함수



### 10. 참고(추가 배열 문법)

@@@@@@@@@@@@@@@@[46]~[47]



### 11.참고(콜백함수 구조를 사용하는 이유, 배열은 객체다)

@@@@@@@@@@@@@@@@[48]~[51]



### 12. 참고(new 연산자)

​	@@@@@@@@@@@@@@@@[32]~[34]