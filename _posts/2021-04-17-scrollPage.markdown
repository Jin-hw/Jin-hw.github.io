---
layout: post
title:  "[Interactive] scrollTop 스크롤 바로 현재 페이지 확인"
subtitle:   "Interactive"
categories: develop
tags: front
comments: true
---

# 스크롤로 페이지 분할 하기
---
section 태그로 구분하여 페이지를 나타낼 수 있다.
```HTML
<section>
</section>

<section>
</section>

<section>
</section>
```

```CSS
section {
        position: relative;
        height: 100vh;
        width: 100vw;
        border-top: 1px dashed #333;
      }
```

```javascript
window.addEventListener("scroll", function(event){
      var scroll = this.scrollY;

      for(var i=0; i<totalNum; i++){
        if(scroll > section[i].offsetTop - window.outerHeight/3  && scroll < section[i].offsetTop - window.outerHeight/3 + section[i].offsetHeight){
          pageNum = i;
          break;
        }
      }
      pageChangeFunc();
    });
```
![그림 1-1](/assets/img/web/2021-03-22/1-14.png)

## 코드 분석
---
### 페이지 크기 
---
- section[i].offsetTop - window.outerHeight/3 은 한페이지(section)의 offsetTop에서 창(window.outerHeight)의 1/3 길이 만큼을 빼줘서 다음 페이지의 offsetTop이 창의 윗부분에 닿지않아도 페이지 수와 배경색이 바뀔 수 있게 만들어준다.

- section[i].offsetTop - window.outerHeight/3 + section[i].offsetHeight 은
한 페이지의 offsetTop에서 창의 1/3을 뺸 것에서 한 페이지(offsetHeight) 높이만큼 더해준다.

따라서 실제 경계선은 화면에 보이는 페이지의 경계선 보다 1/3페이지 만큼 올라가 있다.

### 페이지 번호
---
for문을 사용해서 if의 조건에 해당하는 페이지에 도착하면 break로 루프문을 빠져나간다.

스크롤을 내릴 때마다 이벤트가 발생(for문도 스크롤을 내릴 때마다 실행)하는데 scroll의 값에 따라서 현재 몇 페이지에 있는지 확인을 한다. 따라서 if문을 만족하면 해당 페이지에 해당하는 i를 구할 수 있다.