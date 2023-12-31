# Style Guide

## 파이썬 Style Guide

    * 변수명은 무엇을 위한 변수인지 직관적인 이름을 가져야 함
    * 공백(spaces) 4칸을 사용하여 코드 블록을 들여쓰기
    * 한 줄의 길이는 79자로 제한하며, 길어질 경우 줄 바꿈을 사용
    * 문자와 밑줄(_)을 사용하여 함수, 변수, 속성의 이름을 작성
    * 함수 정의나 클래스 정의 등의 블록 사이에는 빈 줄을 추가
    * ...
    * 참고 : https://peps.python.org/pep-0008/

## 변수명 Guide

    1. 해당 값이 **True, False 를 의미하는 거면 변수명에 is**를 붙히는게 개발자 관례.  
    　　　ex) is_result

    2. **단수, 복수 구분**도 중요함.  
    　　　ex) [1, 2, 3, 4, 5]  리스트의 경우 변수명은 number 보다 **numbers**가 좋음

    3. **상수**(코드 내에서 변하지 않는 값)는 변수를 **대문자**로 저장하는게 개발자 관례.  
    　　　ex) SECONDS_PER_MINUTE = 60

    4. 기본적으로 연산자 양 옆으로는 한칸씩 띄우는게 관례임  
    　　　ex)  2 + 3 * (4 - 5) / 2
