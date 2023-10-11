# Many to one relationships(N:1)

### 1. Many to one relationships(N:1)

- 한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 관계
- Comments - Article(게시글 - 댓글, N:1 관계)
  -  0개 이상의 댓글이 1개의 게시글에 작성 될 수 있다.
- ForeignKey() 
  - N : 1 관계 설정 모델 필드

### 2. 게시글 댓글 만들기

​	(1)  댓글 모델 정의

​		<span style = "color:red">[12] page img</span>  

> ForeignKey(to, on _delete)
>
> - to : 참조하는 모델 calss 이름
> - on_delete : 외래 키가 참조하는 객체(1)가 사라졌을 때, 외래 키를 가진 객체(N)를 어떻게 처리할 지를 정의하는 설정(데이터 무결성)
> - on_delte의 'CASCADE' 설정 : 부모 객체(참조 된 객체)가 삭제 됐을 때 이를 참조하는 객체도 삭제

​	(2) 댓글 생성 연습

​		<span style = "color:red">[19~25] page img</span>  

### 3. 역참조

- N:1 관계에서 1에서 N을 참조하거나 조회하는 것 (1 → N)
- (ex) 해당 게시글에 작성된 모든 댓글을 조회
- N은 외래 키를 가지고 있어 물리적으로 참조가 가능하지만, 1은 N에 대한 참조 방법이 존재하지 않아 별도의 역참조 이름이 필요

```txt
#역참조 사용 예시
article.comment_set.all()
: 모델 인스턴스 - related manager(역참조 이름)- Queryset API
```

​	(1) related manager

​		● N:1 혹은 M:N 관계에서 역참조 시에 사용하는 매니저

​		●'objects' 매니저를 통해 queryset api를 사용했던 것처럼 realated manager를 통해 queryset api를 사용할 수 있게 됨

​	(2) related manager 이름 규칙	

​		● N:1 관계에서 생성되는 Related manager의 이름은 참조하는 "모델명_set"이름 규칙으로 만들어짐 

​		● 게시글의 댓글 목록(Aritlce → Comment)

​			: article.comment_set.all()

### 4. 댓글 CREATE 구현

<span style = "color:red"> [38~47] page img </span> 