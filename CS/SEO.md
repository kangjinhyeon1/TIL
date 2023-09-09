# SEO(검색엔진 최적화)

<aside>
💡 짧 설명: SEO는 검색엔진 최적화를 의미하며 웹 기반 서비스를 운영할 때 반듯이 고려해야하는 한다.

</aside>

## SEO를 고려해서 웹 서비스를 만들어야하는 이유??

> 웹 서비스를 만들 때 다양한 기능들이 많고
사용자가 사용하기 편하도록 만드는 것이 매우 중요하다.
하지만 사용자들에게 내가 만든 웹 서비스를 찾을 수 있도록 검색엔진에 노출 시는 것 또한 매우 중요하다.
> 

만약 궁금한 것이 생겨 구글에 검색을 했을 때 특정 키워드를 입력 후 사람들은 가장 상위에 노출된 페이지를 열람하게 된다. 이때 검색엔진 결과 페이지에서 웹사이트 또는 웹페이지의 상위 노출도를 높이는 작업이 SEO입니다.

![SEO.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2891bd9d-bdf7-4986-a5a5-dae5abfb44ca/SEO.png)

- 위와 같이 상위 노출 되는 검색 결과는 2개가 있다.
- organic Search는 자연 검색된 결과로 일반사용자들이 올린 결과이다.
- pay-per-click은 광고로 노출되는 결과로 대부분의 유료광고는 결과 상단과 하단에 위치해 있다.

## 검색엔진 최적화하는 방법!!

> html을 공부 할 때 <head>태그에 들어가는 부분이 중요 하지 않다고 생각할 수 있지만 사실 여기 부분도 굉장히 중요하다!! 왜냐? 이 검색엔진을 최적화를 할 수 있는 유일한 부분이기 때문이다.
> 

### ❗메타태그(Meta-Tag)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/425b0bf2-b3d5-45c4-b7e2-9ea77b6c0795/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3395f390-13b9-4ffc-8596-6b76093b9f0d/Untitled.png)

**<title> 태그**

실제 구글이나 네이버 검색을 할 때 대부분 제목을 검색해 결과를 찾는 경우가 대다수 이며 검색 결과 또한 제목이 가장 크게 보이며 중요도가 굉장히 높다.

```jsx
<title>프론트엔드 강의 - 추천순 프론트엔드</title>
```

- 위 와 같은 방식으로 코드를 작성하며 title요소를 정의할 때는 너무 긴 텍스트를 사용하거나 모든 웹페이지의 title에 단일 제목을 사용하지 않도록 유의 해야한다.

**<description> 태그**

메타 태그중 title태그 만큼 중요한 태그이며 해당 웹페이지에 설명을 요약하여 한 두 줄의 문장을 의미한다. 대부분의 사용자는 디스크립션을 확인후 자신이 찾고 있던 정보가 담겨있는지 아닌지를 판단한다. 따라서 최대한 잘 읽히는 문장으로 작성해야한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e28a69c6-646c-4615-9f3d-9188156dd2d9/Untitled.png)

```jsx
<meta content="오늘도 굉장히 힘들고 어썸한 수업을 듯고 계시는군요 히히" name="description">
```

**<robots>태그**

메타 태그 중 로봇 태그는 웹페이지 별 검색 로봇의 접근 여부를 설정할 때 사용한다. 일반적으로는 각 검색엔진에는 웹페이지를 크롤링하는 검색 로봇이있다. *여기서 크롤링의 의미는, 검색 로봇들이 내 웹페이지를 돌면서 데이터를 수집하는것을 의미한다.* 그리고 일반적으로는 검색 결과에 노출되는 콘텐츠들은 크롤링 과정과 색인 과정을 거친다.

하지만 로봇태그의 속성을 어떻게 정의하느냐에 따라 이 검색 로봇이 웹페이지를 크롤링하고 색인 할 수 있는 권한을 받거나 못 받을 수 도 있다.

```jsx
<meta content="noodp" name="robots">
```

**canonical 태그**

캐노니컬 태그는 여러 URL을 가진 웹페이지가있을 때, 해당 페이지의 대표 URL을 설정 할 수 있는 태그이다.

이뿐만이 아니라 한 페이지의 대표되는 URL을 지정함으로써, 검색 로봇이 웹페이지를 크롤링할 때 중복URL로 인한 페널티가 적용되게 하지 않게끔 도와준다.

```jsx
<link href="https://www.inflearn.com" rel="canonical">
```

**오픈 그래프(Open Graph) 태그**

오픈 그래프 태그는 웹페이지의 링크가 카카오톡이나 기타 SNS에서 공유될 때 어떻게 노출될지를 정의해주는 역할을 한다. 단순히 SNS에서만 효과적으로 전달 할 수 있는 것이 아닌 검색엔진 최적화 과정에서 해당 웹 페이지가 얼마나 공유되고있는지 파단하는 기준이 되어 검색 상위 노출을 위한 품질 평가에도 영향을 준다.

오픈 그래프 태그는 og:의 형태로 나타낸다.

```jsx
<meta property="og:url" content="https://www.inflearn.com/courses/it-programming/front-end">
<meta property="og:type" content="website">
<meta property="og:description" content="관심 있는 강의가 있다면 지금 당장 시작하세요! 인프런은 언제나 당신의 성장을 응원합니다. - 학습하기 | 인프런">
```

코드는 위와 같은 방식으로 작성한다.

- og:title: 웹페이지 제목
- og:description: 웹페이지 상세 설명
- og:image: 웹페이지 카드에 나타나는 썸네일
- og:type: 웹페이지 유형
- og:url: 웹페이지 주소