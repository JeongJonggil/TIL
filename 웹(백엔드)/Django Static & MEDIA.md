# Django Static & MEDIA

### 0. 원리

- #### Client와 Server 사이에서 어떠한 파일을 제공하려면 요청에 응답하기 위한 URL이 필요함

- #### Client가 웹 페이지를 통해 확인할 수 있는 내용들은 모두 URL 주소를 통해 server에 요청을 하고 제공받은 것들임

- #### 그래서 결국 static 파일도 url 주소가 생성됨

  

### 1. Static Files(정적 파일)

- ##### 서버 측에서 변경되지 않고 고정적으로 제공되는 파일(이미지, JS, CSS 파일 등)

  

### 2. Static files 사용법

- ##### django에서 static 파일은 위치를 아무데나 두고 경로를 적어두어도 인식하지 못함.

- ##### 따라서 아래 규칙들과 3.Static files의 경로에 관한 규칙들을 명확히 준수해야 됨

- ##### static 파일들은 django에서 직접적인 물리적인 주소로 가져올 수 없음 → static 태그를 사용해야됨

- ##### static 태그는 django에 built-in 되어 있지 않으므로 import하는것 처럼 load를 하고 사용 해야함

  ```html
  (ex)
  
  {% load static %} → static 태그를 사용하려면 해당하는 html에서 load를 선언한 후에 사용해야 함
  
  1. <a href="articles/sample-1.png"></a> → X (물리적인 주소)
  2. <a href="{% static "articles/sample-1.png" %}"></a> → O (static 태그)
  ```



### 3. Static files 경로

##### 	(1) 기본경로: app폴더/static 

​		→ 기본 경로는 dajngo에서 static 파일을 찾을때 입력하지 않아도 자동으로 인식가능한 경로

​		→ 따라서 templates 처럼 **(app폴더/static)/app폴더/파일** 이렇게 파일이 위치하게 함

##### 	(2) 추가경로: STATICFILES_DIR에 문자열 값으로 추가 경로 설정

​		→  STATICFILES_DIR : 정적 파일의 기본 경로 외에 추가적인 경로 목록을 정의하는 리스트(리스트이므로 경로 여러개 작성 가능)

```
#settings.py에 작성
→ static 파일을 찾을때(static 테그 사용시) django에서 작성된 경로까지는 자동으로 인식함

STATICFILES_DIR = [
	BASE_DIR/'static1', #BASE_DIR내 static1 폴더까지는 자동으로 인식
	BASE_DIR/'static2', #BASE_DIR내 static2 폴더까지는 자동으로 인식
		  ●
		  ●
]
```



### 4. Static URL

- 기본 경로 및 추가 경로에 위치한 정적 파일을 참조하기 위한 URL. 
- 실제 파일이나 디렉토리가 아니며, URL로만 존재
- project의 setting.py에서 STATIC_URL 부분을 통해 생성되는 url 주소를 설정 가능함

> **생성되는 static 파일의 URL : URL + STATIC_URL + 정적파일 경로**
> 	**(ex) http://127.0.0.1:8000/static/articles/sample-1.png** 

