# 관통 PJT 05 (크롤링)

### 1. 파이썬으로 웹 페이지에 있는 정보를 가져오는 방법

##### <span style= "color:red">[1] img </span>

### 2. 웹 크롤링 이해하기

​	(1) 데이터 사이언스 프로세스

​		<span style= "color:red">[2] img </span>

​	(2) 데이터 수집

​	<span style= "color:red">[3] img </span>

### 3. 웹 크롤링

- 여러 웹 페이지를 돌아다니며 원하는 정보를 모으는 기술
- 원하는 정보를 추출하는 스크래핑( Scraping) 과 여러 웹 페이지를 자동으로 탐색하는 크롤링(Crawiling) 의 개념을 합쳐 웹 크롤링이라고 부름
- 즉, 웹 사이트들을 돌아다니며 필요한 데이터를 추출하여 활용할 수 있도록 자동화된 프로세스



### 4. 웹 크롤링 프로세스

​		<span style= "color:red">[4] img </span>

​		<span style= "color:red">[5] img </span>

​		<span style= "color:red">[6] img </span>



- 크롤링 예시 코드 1 (BeautifulSoap 사용 실습)

```python
import requests
from bs4 import BeautifulSoup

def crawling_basic():
    # 가져올 웹 페이지 url
    url = 'https://quotes.toscrape.com/tag/love/'
    response = requests.get(url)

    # 우리가 얻고자 하는 HTML 내용이 여기에 담긴다.
    html_text = response.text

    # HTML을 파싱이 가능한 정리된 형태로 반환
    soup = BeautifulSoup(html_text,'html.parser')

    # 예쁘게 출력하기
    print(soup.prettify())

    # 1. 태그로 검색하기
    # 크롤링 할 때는 항상 페이지 분석 -> 검색
    # 1.1 가장 첫 번째 태그에 해당하는 요소
    # .text는 a태그에 있는 content 내용만 들고오는 거
    title = soup.find('a')
    print(f'제목 : {title.text}')


    # 1.2 해당 태그 모든 요소
    a_tags = soup.find_all('a')
    for a_tag in a_tags:
        print(f'a 태그들 : {a_tag}')


    # 2 CSS 선택자로 검색하기
    # 2.1 첫 번째로 CSS 선택자와 일치하는 요소
    word = soup.select_one('.text')
    print(f'첫 번째 글 = {word.text}')


    # 2.2 CSS 선택자와 일치하는 모든 요소
    words = soup.select('.text')
    for w in words:
        print(f'글 : {w.text}')


    # 파일로 저장하기
    with open('soup.txt','w',encoding='utf-8') as file:
        file.write(soup.prettify())
    
crawling_basic()
```

- 크롤링 예시 코드 2 (Selenim 사용 실습)

```python
# Selenium 사용 실습
# Selenium : 동적 페이지, 즉 자바스크립트가 다 실행된 후의 html 데이터를 가지고 오게 해주는 라이브러리

from bs4 import BeautifulSoup
from selenium import webdriver

def get_google_data(keyword):
    url = f'https://www.google.com/search?q={keyword}'
    
    
    # 크롬 브라우저가 열림
    # 이 때, 동적인 내용들이 모두 채워진다!
    driver = webdriver.Chrome()
    driver.get(url)
    
    # 열린 페이지 소스를 받아옴
    html = driver.page_source
    soup = BeautifulSoup(html, 'html.parser')

    # 검색 결과 가져오기
    # div 태그 안의 id가 result-stats 라는 요소
    result_stats = soup.select_one("div#result-stats")
    print(result_stats.text)

get_google_data('파이썬')
```

- 크롤링 예시 코드 3 (Selenim 사용 실습)

```python
from bs4 import BeautifulSoup
from selenium import webdriver

def get_google_data(keyword):
    url = f'https://www.google.com/search?q={keyword}'
    
    # 크롬 브라우저가 열림
    # 이 때, 동적인 내용들이 모두 채워진다!
    driver = webdriver.Chrome()
    driver.get(url)

    # 열린 페이지 소스를 받아옴
    html = driver.page_source
    soup = BeautifulSoup(html, "html.parser")

    # 결과물 제목들을 뽑아보자!
    # 1. div 태그 중 g class 를 가진 모든 요소 선택
    g_list = soup.select("div.g")
    for g in g_list:
        # 요소 안에 LC20lb MBeuO DKV0Md class 를 가진 특정 요소
        title = g.select_one(".LC20lb.MBeuO.DKV0Md")
        # 결측치 처리
        if title is not None:
            print(f'제목 = {title.text}')

get_google_data('파이썬')
```

