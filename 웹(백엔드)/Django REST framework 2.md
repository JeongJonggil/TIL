# Django REST framework 2

### 1. DRF with N:1 Relation

- URL및 HTTP requests methods 설계

@@@@@@@@@@@@[1]@@@@@@@@@@@@@@@

- GET
  - @@@@@@@@@@[2]~[5]@@@@@@@@@@@@@@

- POST
  - @@@@@@@@@@[6]~[9]@@@@@@@@@@@@@@

- DELETE & PUT
  - @@@@@@@@@@[10]@@@@@@@@@@@@@@

### 2. 응답 데이터 재구성

- 댓글 조회 시 게시글 출력 내역 변경

  > # ※참고(궁금해서 찾아본거) -> 여기 적은 내용 재검토 필요※
  >
  > 하기 이미지 코드 중 article = ArticleTitleSerializer(read_only =True)를 보면, article 필드는 사용자가 정의한 ArticleTitleSerializer의 인스턴스로 만들놓고 views.py에서 serialize를 진행할 때 Article. 그런데 ArticleTitleSerializer 매개변수를 보면 어떤 데이터를 serialize해야하는지에 대한 data 매개변수가 전달되지 않고있음. 그런데 어떻게 정상적으로 동작하는 건지?
  >
  > → Chatgpt 답변
  >
  > 답은 DRF의 내부 메커니즘에 있습니다.
  >
  > 1. **Field Initialization**: `CommentSerializer`가 초기화될 때 (즉, 객체가 생성될 때), DRF는 각 필드에 대한 초기화도 수행합니다. 이때 `article` 필드는 `ArticleTitleSerializer`의 인스턴스로 초기화됩니다.
  > 2. **Accessing Object Attributes**: `CommentSerializer`가 `Comment` 인스턴스를 serialize할 때, DRF는 해당 인스턴스의 각 필드 값을 가져오기 위해 해당 필드 이름을 속성 이름으로 사용합니다. 예를 들어, `comment.article`는 `Comment` 인스턴스의 `article` 필드 값을 반환합니다.
  > 3. **Field-level Serialization**: DRF는 각 필드 값을 해당 필드의 serializer를 사용하여 serialize합니다. `article` 필드의 경우, DRF는 `ArticleTitleSerializer`를 사용하여 `comment.article` 값을 serialize합니다.
  > 4. **Passing Data to Nested Serializer**: `ArticleTitleSerializer`가 `article` 값을 serialize할 때, DRF는 `comment.article` 값을 해당 serializer의 인스턴스에 전달합니다. 이때 별도의 매개변수 전달은 필요 없습니다. DRF가 내부적으로 필드 값을 해당 serializer에 전달하는 메커니즘을 가지고 있기 때문입니다.

  - @@@@@@@@@@[11]~[12]@@@@@@@@@@@@@@

### 3. 역참조 데이터 구성

- comment_set = CommentSerializer(many=True, read_only=True)
  - comment_set 필드 이름은 model에서 ManyToManyField의 realated_name 속성을 설정하지 않는 이상 comment_set 명칭을 사용해야 함. 위의 ※참고※ 2번 부분 참고하면 이해 됨 
  - many = True의 경우 1 → N을 참조하기 때문에 쿼리셋이 복수의 결과를 가져올 수 있어서 many=True 속성을 넣어주어야 함
- comment_count = serializers.IntegerField(source='comment_set.count', read_only =True)
  - comment_count의 명칭은 아무렇게 적어도 됨 → 신규 필드를 생성하는 거기 때문
  - source='comment_set.count'에서 'comment_set.count'는 article.comment_set.count()인데 Meta model 에 Article이 되어 있어서 article은 내부적으로 자동으로 인식해서 생략하고 DRF 문법에 맞게 comment_set.count이 되는 로직임 -> **여기 적은 내용 재검토 필요**

@@@@@@@@@@[13]~[17]@@@@@@@@@@@@@@



#### 4. API 문서화

- OPenAPI Specification(OAS)
  - RESTful API를 설명하고 시각화하는 표준화된 방법
  - API에 대한 세부사항을 기술할 수 있는 공식 표준

- Swagger & Redoc
  - OAS 기반 API에 대한 문서를 생성하는데 도움을 주는 오픈소스 프레임워크

- API 문서화

@@@@@@@@@@[18]~[22]@@@@@@@@@@@@@@

- OAS의 핵심 이점 

@@@@@@@@@@[23]@@@@@@@@@@@@@@



### 5. Django shortcuts functions

- get_object_or_404()
  - 모델 manager objects에서 get()을 호출하지만, 해당 객체가 없을 땐 기존 DoesNotExist 예외(서버를 종료시켜버림) 대신 Http404(서버를 끄지 않고 상태코드를 제공)를 raise 함

- get_list_or_404()
  - 모델 manager objects에서 filter()의 결과를 반환하고, 해당 객체 목록이 없을 땐 Http404를 raise 함 (서버를 종료시켜버리는 대신 서버를 끄지 않고 상태코드를 제공)

- **사용 이유 : 클라이언트에게 "서버에 오류가 발생하여 요청을 수행할 수 없다(500)"라는 원인이 정확하지 않은 에러를 제공하기 보다는, 적절한 예외 처리를 통해 클라이언트에게 보다 정확한 에러 현황을 전달하는 것도 매우 중요한 개발 요소 중 하나이기 때문**