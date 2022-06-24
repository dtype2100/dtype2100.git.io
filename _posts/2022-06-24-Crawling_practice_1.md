---
layout: single
title:  "BeautifulSoup 네이버 뉴스 크롤링 및 AttributeError: 'list' object has no attribute 'text' 해결"
---
# 네이버 뉴스 크롤링 및 에러 해결 방법

파이썬을 활용해서 크롤링 하는 방법을 알아본다. 

BeautifulSoup을 활용해서 진행하며 단계별로 하나씩 확인한다. 

간단한 순서는 다음과 같다.

1. 환경설정
2. URL 정보 받아오기
3. 필요한 데이터 선택
4. 필요한 데이터 출력

# 환경 설정


```python
import requests
from bs4 import BeautifulSoup as bs
```

requests를 import하는 이유는 서버에 요청해야하기 때문이다. 

web에는 서버(Server)와 클라이언트(Client)라는 것이 있다. 서버는 웹에서 필요한 것을 제공하는 쪽이고, 클라이언트는 제공 받는 쪽이다.

크롤링으로 데이터를 가져오기 위해 서버에 데이터를 요청해야하는데, 그 기능을 하는 것이 바로, 'requests'라는 라이브러리다.

단순히 requests만 사용하면 가공되지 않은 코드만 가져오게 된다. 그렇기 때문에 필요한 데이터만 선별해서 가져와야하는데, 이것을 파싱(Parsing)이라 부른다.

파이썬에서 파싱은 BeautifulSoup로 한다.





# URL 정보 받아오기


```python
url = "https://search.naver.com/search.naver?sm=tab_hty.top&where=news&query=%EB%8F%84%EC%8B%9C&oquery=%EC%B7%A8%EC%97%85&tqi=hrR8olp0JXVsstUsZ38ssssssWC-140887"
reponse = requests.get(url)
soup = bs(reponse.text, 'html.parser') # html을 파싱한다는 의미로 'html.parser' 입력
```

# 필요한 데이터 선택


```python
title_tags = soup.select('.news_tit') # 네이버 뉴스 제목 선택
```

파이썬은 .select() 매소드를 사용할 수 있다. 괄호() 안에 CSS 선택자를 입력하면 HTML 태그만 선택할 수 있다. 

여기서는 네이버 뉴스의 제목만 선택하기 때문에, 위와 같이 .news_tit만 입력한다.


```python
title_tags
```

title_tags를 출력하면 아래와 같이 나온다.


    [<a class="news_tit" href="https://imnews.imbc.com/news/2022/world/article/6381489_35680.html" onclick="return goOtherCR(this, 'a=nws*h.tit&amp;r=1&amp;i=88000119_000000000000000001204564&amp;g=214.0001204564&amp;u='+urlencode(this.href));" target="_blank" title="[World Now] 전 세계에서 가장 살기 좋은/힘든 도시는?">[World Now] 전 세계에서 가장 살기 좋은/힘든 <mark>도시</mark>는?</a>,
     <a class="news_tit" href="http://www.munhwa.com/news/view.html?no=2022062401039907008002" onclick="return goOtherCR(this, 'a=nws*a.tit&amp;r=6&amp;i=880000C4_000000000000000002519142&amp;g=021.0002519142&amp;u='+urlencode(this.href));" target="_blank" title="롯데건설, 도시정비사업 약 3조 원 수주 눈앞">롯데건설, <mark>도시</mark>정비사업 약 3조 원 수주 눈앞</a>,
     <a class="news_tit" href="http://www.newsis.com/view/?id=NISX20220624_0001919184&amp;cID=14001&amp;pID=14000" onclick="return goOtherCR(this, 'a=nws*a.tit&amp;r=11&amp;i=88000127_000000000000000011265717&amp;g=003.0011265717&amp;u='+urlencode(this.href));" target="_blank" title="성남시, 유네스코 창의도시 ‘미디어아트 분야’ 선정">성남시, 유네스코 창의<mark>도시</mark> ‘미디어아트 분야’ 선정</a>,
     <a class="news_tit" href="http://www.inews24.com/view/1493758" onclick="return goOtherCR(this, 'a=nws*a.tit&amp;r=16&amp;i=880000D6_000000000000000000680932&amp;g=031.0000680932&amp;u='+urlencode(this.href));" target="_blank" title="롯데건설, 도시정비사업 3조 클럽 진입 육박">롯데건설, <mark>도시</mark>정비사업 3조 클럽 진입 육박</a>,
     <a class="news_tit" href="https://www.yna.co.kr/view/AKR20220624033600051?input=1195m" onclick="return goOtherCR(this, 'a=nws*a.tit&amp;r=21&amp;i=880000D8_000000000000000013266560&amp;g=001.0013266560&amp;u='+urlencode(this.href));" target="_blank" title="부산 도시철도 차량 실내 공기질 '양호'">부산 <mark>도시</mark>철도 차량 실내 공기질 '양호'</a>,
     <a class="news_tit" href="https://www.news1.kr/articles/?4721793" onclick="return goOtherCR(this, 'a=nws*a.tit&amp;r=25&amp;i=08138263_000000000000000006177077&amp;g=421.0006177077&amp;u='+urlencode(this.href));" target="_blank" title="1200만 앞둔 '범죄도시2' 필리핀서 개봉…성황리 시사회 마쳐">1200만 앞둔 '범죄<mark>도시</mark>2' 필리핀서 개봉…성황리 시사회 마쳐</a>,
     <a class="news_tit" href="https://www.ajunews.com/view/20220624094030803" onclick="return goOtherCR(this, 'a=nws*f.tit&amp;r=30&amp;i=8800058B_000000000000000002146449&amp;g=5090.0002146449&amp;u='+urlencode(this.href));" target="_blank" title="인천도시공사, 검단신도시 도로 확장공사 착공">인천<mark>도시</mark>공사, 검단신<mark>도시</mark> 도로 확장공사 착공</a>,
     <a class="news_tit" href="https://news.kbs.co.kr/news/view.do?ncd=5493978&amp;ref=A" onclick="return goOtherCR(this, 'a=nws*e.tit&amp;r=31&amp;i=88000114_000000000000000011290030&amp;g=056.0011290030&amp;u='+urlencode(this.href));" target="_blank" title="[지구촌 더뉴스] 전 세계 가장 살기 좋은 도시 1위는?">[지구촌 더뉴스] 전 세계 가장 살기 좋은 <mark>도시</mark> 1위는?</a>,
     <a class="news_tit" href="https://www.yna.co.kr/view/AKR20220624047700005?input=1195m" onclick="return goOtherCR(this, 'a=nws*e.tit&amp;r=32&amp;i=880000D8_000000000000000013266984&amp;g=001.0013266984&amp;u='+urlencode(this.href));" target="_blank" title="[신간] 유럽도시기행 2">[신간] 유럽<mark>도시</mark>기행 2</a>,
     <a class="news_tit" href="https://www.donga.com/news/article/all/20220623/114075206/1" onclick="return goOtherCR(this, 'a=nws*j.tit&amp;r=33&amp;i=880000A9_000000000000000003436018&amp;g=020.0003436018&amp;u='+urlencode(this.href));" target="_blank" title="팍팍한 도시 떠나 시골로…귀농·귀촌 가구 역대 최대">팍팍한 <mark>도시</mark> 떠나 시골로…귀농·귀촌 가구 역대 최대</a>]



이제 크롤링이 끝날줄 알았는데, 출력하면 위와 같이 확인하기 어려운 형태로 나오게 된다. 

그렇기에 이제 출력한 데이터를 문자로 추출할 수 있도록 해야 한다.


```python
title_tags.text
```


    ---------------------------------------------------------------------------
    
    AttributeError                            Traceback (most recent call last)
    
    <ipython-input-5-ce0669f49b61> in <module>()
    ----> 1 title_tags.text
    AttributeError: 'list' object has no attribute 'text'


    AttributeError: 'list' object has no attribute 'text'



.text를 사용하면 문자만 꺼내올 수 있는데, 단순히 위와 같은 코드만 사용하면, 에러가 발생한다.



```python
print(title_tags.text)
```


    ---------------------------------------------------------------------------
    
    AttributeError                            Traceback (most recent call last)
    
    <ipython-input-11-3acd4e102a32> in <module>()
    ----> 1 print(title_tags.text)


    AttributeError: 'list' object has no attribute 'text'


print 함수를 사용해서 다시 출력해 봤지만 마찬가지로 에러가 발생한다.

에러를 보면, 리스트는 text를 가질 수 없다고 한다.

그래서 출력하려는 값의 위치를 다시 설정해서 시도하면 아래와 같이 나오는 것을 확인할 수 있다.


```python
print(title_tags[0].text)
```

    [World Now] 전 세계에서 가장 살기 좋은/힘든 도시는?



0번째 위치에 있는 값을 출력하기 위해 0을 입력하면 위와 같은 결과가 나온다.

이로써 출력하려는 값의 위치만 입력하면 원하는 값을 출력할 수 있다는 것을 알게 되었다.



```python
print(title_tags[0].text)
print(title_tags[1].text)
print(title_tags[2].text)
```

    [World Now] 전 세계에서 가장 살기 좋은/힘든 도시는?
    롯데건설, 도시정비사업 약 3조 원 수주 눈앞
    성남시, 유네스코 창의도시 ‘미디어아트 분야’ 선정


print함수를 사용해서 위와 같이 출력하면 3번째 제목까지 나오는 것을 볼 수 있다.

그런데 효율성을 위해서라도 반복해서 같은 업무를 수행하는 자동화 코드를 구성할 필요가 있다.

아래 코드를 통해 확인해 본다.

# 반복해서 필요한 데이터 출력


```python
title = []
for tag in title_tags:
  title.append(tag.text)

print(title)
```

    ['[World Now] 전 세계에서 가장 살기 좋은/힘든 도시는?', '롯데건설, 도시정비사업 약 3조 원 수주 눈앞', '성남시, 유네스코 창의도시 ‘미디어아트 분야’ 선정', '롯데건설, 도시정비사업 3조 클럽 진입 육박', "부산 도시철도 차량 실내 공기질 '양호'", "1200만 앞둔 '범죄도시2' 필리핀서 개봉…성황리 시사회 마쳐", '인천도시공사, 검단신도시 도로 확장공사 착공', '[지구촌 더뉴스] 전 세계 가장 살기 좋은 도시 1위는?', '[신간] 유럽도시기행 2', '팍팍한 도시 떠나 시골로…귀농·귀촌 가구 역대 최대']



```python
title
```

title을 출력하면 아래와 같이 나온다.


    ['[World Now] 전 세계에서 가장 살기 좋은/힘든 도시는?',
     '롯데건설, 도시정비사업 약 3조 원 수주 눈앞',
     '성남시, 유네스코 창의도시 ‘미디어아트 분야’ 선정',
     '롯데건설, 도시정비사업 3조 클럽 진입 육박',
     "부산 도시철도 차량 실내 공기질 '양호'",
     "1200만 앞둔 '범죄도시2' 필리핀서 개봉…성황리 시사회 마쳐",
     '인천도시공사, 검단신도시 도로 확장공사 착공',
     '[지구촌 더뉴스] 전 세계 가장 살기 좋은 도시 1위는?',
     '[신간] 유럽도시기행 2',
     '팍팍한 도시 떠나 시골로…귀농·귀촌 가구 역대 최대']




위와 같이 for문을 사용하면 자동으로 네이버 뉴스 제목이 출력되는 것을 볼 수 있다.

출력하려는 값의 위치를 따로 설정하지 않더라도 에러가 발생하지 않은 것은 for문 덕분인 것으로 보인다.

for문을 활용하면 in 안에 있는 범위 내에서 자동으로 텍스트만 선택해서 출력해 주기 때문으로 보인다.

