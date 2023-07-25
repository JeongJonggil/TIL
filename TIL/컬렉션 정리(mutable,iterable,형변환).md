# 컬렉션 정리(mutable, iterable, 형변환, 내부요소 )

### 1. mutable, iterable(→sequance이면 iterable임)

    **(1) mutable** : 객체의 상태를 변경해도 메모리에서 같은 주소를 유지

    (2) iterable : 반복문에 사용할 수 있으면 iterable하다고 생각하면 됨

![](C:\Users\SSAFY\AppData\Roaming\marktext\images\2023-07-25-09-48-11-image.png)

**********

### 2. 형변환

![](C:\Users\SSAFY\AppData\Roaming\marktext\images\2023-07-25-09-50-17-image.png)

****

### 3. 내부 요소

|            | 숫자  <br>(int, Float 등) | 문자열  <br>(숫자, 문자) | 리스트 | 튜플  | 딕셔너리 | 세트        |
| ---------- | ---------------------- | ----------------- | --- | --- | ---- | --------- |
| Str        | X                      | O                 | X   | X   | X    | X         |
| List       | O                      | O                 | O   | O   | O    | O         |
| Dict_Key   | O                      | O                 | X   | O   | X    | frozenset |
| Dict_Value | O                      | O                 | O   | O   | O    | O         |
| Set        | O                      | O                 | X   | O   | X    | X         |

    (1) Str : 문자열로만 구성 가능

    (2) List, Dict_value: 모든 데이터 타입을 값으로 가질 수 있음

    (3) Dicit_Key, Set  
      : 해쉬 가능한 타입만 가능 → Immutable + 해시 함수를 통해 해시값을 얻을 수 있는 타입
