---
layout: post
title:  "구형 아이폰 스마트 시계로 만들기"
date:   2021-01-02 00:00:00
---
10여년간 거실을 지키던 탁상시계가 고장났다. 숫자가 크게 나와서 마음에 들었던 시계였는데 연말에 동네가 잠시 정전된 사이 완전히 고장나버렸다. 창밖 너머에는 거대한 시계를 벽면에 붙인 대형 빌딩도 있었고 맥북 귀퉁이에도 늘 시계가 표시되어 있으니 집에 시계가 꼭 있어야할까 싶어 새 시계 구매를 미루었지만, 샤워하고 나와서 늘 확인하던 거실 시계가 없어지니 여간 불편한게 아니었다.

스마트 시계를 하나 장만할까 하고 알아보았다. 이 정도 디자인이면 디스플레이를 사다가 내가 만들어도 되겠다 싶었다. 그렇게 디스플레이를 알아보니 예산이 몇십만원으로 불어나기 시작했다.
그러던 와중에 스트리밍 라디오 출력용으로 쓰던 구형 아이폰이 시야에 들어왔다. 집에 굴러다니는 구형 폰이 얼마나 많던가. 구형 아이폰 디스플레이를 탁상시계로 만들어보기로 했다.

<div class="fb-post" data-href="https://www.facebook.com/rainygirl/posts/10159113297774136" data-width="500" data-show-text="true"><blockquote cite="https://www.facebook.com/rainygirl/posts/10159113297774136" class="fb-xfbml-parse-ignore">Posted by <a href="#" role="button">rainygirl</a> on&nbsp;<a href="https://www.facebook.com/rainygirl/posts/10159113297774136">Saturday, January 2, 2021</a></blockquote></div>


# 준비물

- 항상 켜져있는 구형 아이폰
- 항상 켜져있는 홈 서버
- 내부망을 구성할 수 있는 공유기

- 시계를 작동시킬 JS와 HTML 코드
- 날씨를 긁어와 가공해 줄 fastapi/python 코드
- https 프록시 서버로 기능할 stunnel

# 시계 만들기

지하철 도착역을 안내하는 행선안내기가 Internet Explorer 를 띄워 작동하는걸 본 일이 있다. 적당한 키오스크는 웹브라우저 방식으로 만들어도 되겠다고 생각했다. 
Javascript로 시계를 만드는건 매우 쉽다. new Date() 에서 시분값을 가져오면 된다.

### clock.js
```javascript
function getClock(){
  const _=new Date,
      h=_.getHours().toString().padStart(2,'0'),
      m=_.getMinutes().toString().padStart(2,'0');

  return h+m;
}
```

setInterval 로 값을 받아 그려주면 된다.
밋밋하지 않게 DIV 4개에다 숫자를 하나씩 넣고 스타일을 조금씩 바꾸면, 시판되는 스마트시계와 얼추 비슷한 디자인을 꾸밀 수 있다.

# 플립 효과 넣기

그저 숫자만 바뀌면 밋밋하니까, 자릿수마다 DIV를 두개 넣어 숫자가 바뀔 즈음 아래에서 위로 숫자를 밀어내도록 transition을 넣어주었다.

### clock.css
```css
#clock>div{
  position:absolute;
  ...
}
#clock>div>div{
  position:absolute;
  top:0;
  left:0;
  width:100%;
  height:100%;
  transition:transform .4s ease, opacity .4s ease;
  transform:translate3d(0,0,0);
  opacity:1;
}
#clock div.up{
  transform:translate3d(0,-90vh,0);
  opacity:0;
}
#clock div.down{
  transform:translate3d(0,90vh,0);
  opacity:0;
}
```

### clock.js
```javascript
function flip(i){
  const t=document.getElementById(`clock${i}`);
  t.querySelector('.card1').classList.add('up');
  t.querySelector('.card2').classList.remove('down');
}

for(let i=3;i>=0;i--){
  try{
    o=parseInt(document.getElementById(`clock${i+1}`).querySelector('.card2').innerHTML);
  }catch(x){
    o='';
  }
  p=parseInt(c[i]);

  if(o!==p) {
    document.getElementById(`clock${i+1}`).innerHTML=`<div class="card1">${o}</div><div class="card2 down">${c[i]}</div>`;

    window.setTimeout(function(){flip(i+1);},5);
  }
}
```

# 전체화면 어플 띄우기

아이폰에서 전체화면을 사용하는 앱을 만든다고 해서 무조건 Swift나 React Native 코드를 짤 필요는 없다. HTML, CSS, JS로 짠 PWA(Progressive Web Apps)만으로도 주소창을 가리고 전체화면을 차지하는 브라우저 화면을 간단히 띄울 수 있다. 
한때 전체화면 웹앱을 쉽게 만들어준다는 apple-mobile-web-app-capable 같은 메타태그도 있었지만 [다 옛날 이야기다. iOS 8에서 사라졌다.](https://developer.apple.com/library/archive/releasenotes/General/RN-iOSSDK-8.0/) 
요즘에는 PWA 구성을 위한 manifest 를 만들어 구현한다. 우선 아래와 같은 manifest 파일을 만들고,

### manifest.json
```javascript
{
  "name": "rclock",
  "short_name": "rclock",
  "start_url": "/clock",
  "display": "standalone",
  "icons": [{
    "src": "icon.png",
    "sizes": "512x512",
    "type": "image/png"
  }]
}
```

이 manifest 를 HTML에서 아래와 같이 연결해 쓰면 된다.

### index.html
```html
<link rel="manifest" href="./manifest.json">
```

이 웹페이지를 모바일 사파리에서 열고, 하단 공유 버튼을 누르고, [홈 화면에 추가]를 누르면 아이폰 홈 화면에 PWA의 아이콘이 새로 생긴다. 아이콘을 누르면 주소창 없이 전체화면을 차지하는 브라우저 앱 화면이 나온다.


# 홈 서버 장만하기

개발 단계의 아이폰 앱은 USB나 네트워크 등으로 연결된 맥북에서 바이너리를 업로드할 수 있다. PWA는 기본적으로 웹페이지이기 때문에, 브라우저에서 웹 페이지를 연 뒤 절차를 거쳐 앱 아이콘을 설치해야 한다.
아이콘 생성 이후에는 웹서버가 없어도 캐쉬된 데이터가 남아있다면 적당히 앱이 작동할 것이다. 하지만 처음에는 어딘가에서 웹 페이지를 불러와야만 한다. 게다가 날씨 데이터는 캐쉬된 데이터가 아니라 실시간 데이터를 가져와야 한다. 이런 저런 이유로, 처음 웹페이지를 띄우고, 이후 날씨 데이터도 상시 긁어와 가공하여 응답할 간단한 웹 서버가 하나 필요해졌다.

외부 클라우드 등에서 돌고 있는 인스턴스를 썼다간 야금야금 돈도 나가고 관리부담도 생길 것이다. 데이터 수집을 위해 집에서 항상 켜두고 있던 2010년형 맥북을 겸사겸사 홈 서버로 쓰기로 했다. Python/FastAPI로 서버를 하나 띄웠다. 웹페이지는 HTML 코드를 템플릿 엔진 안거치고서 대충 띄우게 했다. HTML 코드를 직접 고치는 것 외에 더 손 볼 일은 없다.

### main.py
```python
from fastapi import FastAPI
from fastapi.responses import HTMLResponse
from fastapi.staticfiles import StaticFiles

import json

app = FastAPI()

app.mount("/i", StaticFiles(directory="html/i"), name="static")

@app.get("/clock")
async def clock():
    with open("html/index.html","r") as fp :
        s=fp.read()

    return HTMLResponse(content=s, status_code=200)

@app.get("/manifest.json")
async def manifest():
    with open("html/manifest.json","r") as fp :
        s=fp.read()

    return json.loads(s)
```

# 날씨 가져오는 API 만들기

날씨는 시시각각 변하기 때문에 주기적으로 AJAX 또는 Fetch 로 가져와야 한다.
날씨 데이터를 제공하는 사이트는 많이 있으며, 이들 데이터를 긁어다가 가공해서 응답하면 된다.

응답 데이터는 아래와 같이 구성했다.

{"currentForecast":"Cloudy","currentFeellike":"-8˚","todayLow":"-9˚","todayHigh":"-2˚"}

시계에는 간단한 최저 기온, 최고 기온, 현재 체감기온, 오늘의 날씨만 나오면 된다. 시계가 정보를 과다하게 제공할 필요는 없다. 내일 날씨는 애플 워치나 iStats Weather, 또는 Spotlight의 날씨, 맥OS 날씨 위젯, 평소에 사용하는 아이폰 날씨 위젯, 말하는 시리, 잠깐 켠 TV뉴스, 라디오 1분 기상정보 등이 알려줄 것이다. 나는 단지, 지금 당장 집밖으로 나가야한다면 대충 후드 뒤집어쓰고 나가도 되는지 패딩을 입고 나가야하는지를 알고싶은 것이다. 그래서, 현재 기온 대신 체감 기온을 가져오고 현재 날씨만 가져오기로 했다. 

### main.py
```python
@app.get("/weather")
async def weather():
    data = requests.get(FORECAST_URL)
    # 크롤링 과정 생략

    return {
        "currentForecast": current_forecast,
        "currentFeellike": current_feellike,
        "todayLow": today_low,
        "todayHigh": today_high}
```

적당히, 60초에 두어번, 5초씩 화면을 넘겨 날씨가 나오도록 했다.


# https 구성하기

아무리 가정용 내부 네트워크라 하더라도 HSTS가 등장한 이래 요즘 브라우저에서 작동하는 모든 Fetch, XMLHttpRequest 는 https 로 구성되어야 한다. 개발서버는 보통 https로 작동하지 않는다. 이 문제를 피할 가장 쉬운 방법은 적당한 도메인을 붙여 https 서버를 구성하는 것이다. 하지만 나는 로컬 네트워크에 서버를 두기로 했기 때문에 도메인까지 씌울 이유는 없었다. SSL 터널링 서버를 붙여 누더기(?) https를 구성하기로 했다.

SSL 터널링 서버는 stunnel을 쓰기로 했다. cert 파일을 만들어야 한다.


```
> openssl genrsa 2048 >stunnel.key
> openssl req -new -x509 -nodes -sha1 -days 3650 -key stunnel.key > stunnel.cert
> cat stunnel.key stunnel.cert > stunnel.pem
```

stunnel 이 참조할 configuration 파일도 하나 만들어야 한다.

## dev_https
```
pid=

cert = stunnel.pem
sslVersion=TLSv1
foreground = yes
output = stunnel.log

[https]
accept=443
connect=8000
TIMEOUTclose=1
```

FastAPI 서버를 띄우고 stunnel을 띄우면 적당히 돌아가는 https 웹서버가 구성된다.

```
> uvicorn main:app --host 0.0.0.0 --reload &
> stunnel dev_https &
```

정식으로 발급된 인증서가 아니니 경고가 뜰 것이다.
개인용으로 쓰는 것이니 변조 여부만 잘 확인하고서 넘어가기로 한다.
외부에 공개되는 서비스는 이렇게 구성하면 안된다.

# 문제점

아이폰6는 LED 백라이트 디스플레이를 쓰지만 그럼에도 불구하고 번인 현상이 있다. 이 문제는 각 시간마다 색상을 바꾸어 대응하기로 했다.

![-](/images/2021-01-02-burn.jpg)

아이폰 이후 기종은 OLED를 쓰기 때문에 번인 현상이 더 심할 수 있다. OLED 사용 기종을 쓰게 된다면 모양을 바꾸는 등 화면보호 과정을 더 포함시켜야 할 것이다.

# 과제

출근 시간대에는 대중교통 도착시간을 시계에다 띄울 수 있을 것이다.
배달음식이 집 근처로 온다면, 곧 도착한다는 알림 정도는 띄울 수 있을 것이다.
운동량이 부족하다면 운동좀 하라고, 수분 섭취가 부족하다면 물 마시라고, 허리가 굽어있으면 허리를 세우라고 잔소리를 할 수도 있을 것이다.
아마도, 애플워치와 비슷한 기능을 하면서도 작업공간이나 거실에 적합한 역할을 맡길 수 있지 않을까 기대된다.

복잡한 브리핑기능까지 넣었다간 '시계'의 본질적 가치에서 벗어나게 된다.
탁상시계란 무엇인가? 자유로이 꾸밀 수 있는 탁상시계는 어떤 모습일때 유익할까? 라는 질문에 우선 답을 할 수 있어야 한다.
머리아픈 고민을 잊고싶을 때, 딴생각 하기에 적당한 과제이다.


