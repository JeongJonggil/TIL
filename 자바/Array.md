# Array

### 1. 배열(Array)

- **같은 종류**의 데이터(자료형/타입)를 저장하기 위한 자료구조
- **크기가 고정**되어 있음 (한번 생성된 배열은 크기를 바꿀 수 없음)
- 배열을 객체로 취급(참조형)
- 길이 변경 필요시 새로운 배열을 생성 후 내용을 옮긴다



### 2. 배열의 선언

- 타입[] 이름 (이 방법을 선호함)
- 타입 이름[]

```java
//1차원 배열을 선언하는 방법
int[] score1;
int score2[];

//배열을 생성하는 방법
//1. 자료형[] 이름 = new 자료형[길이]; 값은 자료형의 초기값으로 초기화 (int 초기값 = 0, str 초기값 = null)
int[] score3 = new int[5];

//2. 자료형[] 이름 = new 자료형[]{1,2,3,4};
int[] score4 = new int[] {1,2,3,4};

//3. 자료형[] 이름 = {1,2,3,4}; //선언과 동시에 초기화
int[] score5 = {1,2,3,4};

//재할당
score3 = new int[6];
score3 = new int[] {1,2,3,4,5};
score3 = {1,2,3,4,5}; //주의! 이건 안됨
```



### 3. 배열의 순회

- for-each

  - for(자료형 변수명 : 반복할수있는것){ }

  ```java
  int[] nums = {1,2,3,4}
  
  for(int n : nums){
  	System.out.println(n);
  }
  
  //배열안의 값이 궁금할 때 배열을 출력하는 방법
  // import java.utill.Arrays; 해야됨
  // 자동 import = ctrl + shift + o
  // 자동 정렬 = ctrl + shift + f
  System.out.println(Arrays.toString(nums));
  
  ```