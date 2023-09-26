# Django Form

### 1. 개요

- ##### html 의 form은 비정상적 혹은 악의적인 요청을 필터링 할 수 없음

- ##### 사용자로부터 받은 데이터에 대해 유효성 검사(형식,중복,범위, 보안 등)를 하기 위해 Django의 Form을 만들어서 사용

### 2. Django Form

- ##### 사용자 입력 데이터를 수집하고, 처리 및 유효성 검사를 수행하기 위한 도구

- ##### 유효성 검사를 단순화하고 자동화 할 수 있는 기능을 제공

- 사용법

  ```python
  1. app에 forms.py 파일 생성
  
  2.forms.py에 하기 코드 작성
  from Django import forms
  
  class ArticleForm(forms.Form):
  	title = forms.CharField(max_length=10)
  	content = forms.CharField()
  	
  3.views.py 중 사용할 함수에 context로 넘겨주기
  from .forms import ArticleForm
  
  def new(request):
  	form = ArticleForm()
  	context = {
  		'form': form,
  	}
  	return render(request,'articles/new.html',context)
  
  4. html에서 변수 표기법(context key)으로 사용하기
  ```

  - ##### Form rendering options

    : label, input 쌍을 특정 HTML태그로 감싸는 옵션

    ex) {{ form.as_p }} → 각 input을 <p>로 감싸서 html에서 줄바꿈을 해서 표기됨

### 3. Widgets

- HTML 'input' element의 표현을 담당
- 단순히 input 요소의 속성 및 출력되는 부분을 변경하는 것

​	ex) content = forms.CharField(widget=forms.Textarea)
​		→ content input 창은 Textarea 박스로 표기 됨

### 4. Django ModelForm

##### 	(1) Form vs ModelForm

​		● Django Form : 사용자 입력 데이터를 DB에 저장하지 않을때

##### 		● Django ModelForm: 사용자 입력 데이터를 DB에 저장해야 할 때 (ex. 회원가입)

##### 	(2) 정의

##### 		●  Model과 연결된 Form을 자동으로 생성해 주는 기능을 제공 Form + Model

##### 	(3) 사용법

```python
1. forsm.py 생성 및 코드 작성
2. 코드
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
	class Meta: 		#Meta는 데이터의 데이터 정도의 의미로 생각하기
		model = Article
		fields = '__all__'
```

##### 	(4) Meta class

​		●  ModelForm의 정보를 작성하는 곳

​		●  'fields' 및 'exclude' 속성 : exlude 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 수도 있음

​	ex) fields =('title',) , exclude = ('title',)



##### 	(5) ModelForm을 적용한 create 로직

![1](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20230926094557397.png)

##### 		●  if form.is_valid(): 를 통과하지 못했을 때는 context 하기 부분이 실행되는데 이 때 자동으로 vaild검사에서 실패힌 이유를 같이 html page에 rendering해줌. 그냥 ModelForm의 특성임

##### 	(6) ModelForm을 적용한 create 로직

![2](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20230926102655789.png)

##### 	(7) ModelForm을 적용한 update 로직

![3](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20230926100536428.png)

​	(8) save() 메서드

![4](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20230926102935599.png)

### 5. HTTP request method 차이점을 활용한 view 함수 구조 변경

![5](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20230926103907287.png)