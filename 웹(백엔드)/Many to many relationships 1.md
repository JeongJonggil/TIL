# Many to many relationships 1

### 1. Many to many relationships (N:M, M:N)

- 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우
  - 양쪽 모두에서 N:1 관계를 가짐



### 2. 환자와 의사 2개의 모델을 사용하여 모델 구조 구상하기

@@@@@@@@@@@@[1]~ [5]img@@@@@@@@@@@@@@@@@@@@

### 

### 3. 중개 모델

@@@@@@@@@@@@@@@[6]~ [8]img@@@@@@@@@@@@@@@@@@@@



### 4. ManyToManyField

- django에서는 위의 중개모델을 ManyToManyField로 자동으로 생성해줌(중개 테이블을 하나 만들어줌)
- N:M 관계에서는 ManyTomanyField를 한쪽에만 필드로 정의하는데 어디쪽에 생성할껀지는 설계자 마음임.

대신 추후 db조회 시 참조와 역참조의 관계를 잘 생각해서 생성해야됨

@@@@@@@@@@@@@@@[9]~ [14]img@@@@@@@@@@@@@@@@@@@@



### 5. 'through' argument

- 중개 테이블에 '추가 데이터'를 사용해 M:N 관계를 형성하려는 경우에 사용

@@@@@@@@@@@@@@@[15]~ [20]img@@@@@@@@@@@@@@@@@@@@



### 6. ManyToManyField arguments

- ManyToManyField(to, **options) : many to many관계 설정 시 사용하는 모델 필드

**(1) related_name : 역참조시 사용하는 manager name을 변경**

```python
ex)
class Patient(models.Model):
	doctors = models.ManyToManyField(Doctor, related_name='patients')

# 변경 전
docotor.patient_set.all()

# related_name 적용 후
docotor.patients.all()
```

**(2) symmetrical options : ManyToManyField가 동일한 모델을 가리키는 정의에서만 사용**

- 기본 값 : True
  - True일 경우
    - source 모델의 인스턴스가 target 모델의 인스턴스를 참조하면 자동으로 target 모델 인스턴스도 source모델 인스턴스를 자동으로 참조하도록 함(대칭)
    - 즉, 자동으로 내가 당신의 친구라면 당신도 내 친구가 됨
  - False일 경우
    - True 였을 때와 반대(대칭되지 않음)

```python
ex)

class Person(models.Model):
	friends = models.ManyToManyField('self')
	# friends = models.ManyToManyField('self',symmetrical=False)
```



### 7. 좋아요 기능

- Article(M) - User(N)
  - 게시글은 회원으로부터 0개 이상의 좋아요를 받을 수 있고, 회원은 0개 이상의 게시글에 좋아요를 누를 수 있음

@@@@@@@@@@@@@@@[21]~ [26]img@@@@@@@@@@@@@@@@@@@@

- **좋아요 기능 구현**

@@@@@@@@@@@@@@@[27]~ [31]img@@@@@@@@@@@@@@@@@@@@