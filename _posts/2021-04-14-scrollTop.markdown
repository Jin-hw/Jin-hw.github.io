---
layout: post
title:  "[Interactive] scrollTop 스크롤 진행 바 나타내기"
subtitle:   "Interactive"
categories: develop
tags: front
comments: true
---

# 스크롤 바로 진행 상황 확인
---
```javascript
    let bar;
    let scrollTop = 0;
    window.onload = function() {
        bar = document.getElementsByClassName("bar")[0];
            
        window.addEventListener("scroll",function(e){
            scrollTop = document.documentElement.scrollTop;
            let per = Math.round(scrollTop / (document.body.scrollHeight - window.innerHeight) * 100);
            console.log(window.innerHeight);
            //console.log(bar)
            bar.style.height = per + "%";
        }, false)
    }
```

## 코드 분석
---
let per = Math.round(scrollTop / (document.body.scrollHeight - window.innerHeight) * 100);

세로 퍼센트값 = 스크롤탑 / (문서 높이 - 화면 높이) * 100;

scrollTop: 스크롤 되어 올라간 만큼의 높이 (스크롤을 한번 굴리면 100씩 움직임)


![그림 1-1](/assets/img/web/2021-03-22/1-13.png)

scrollHeight: body에 속한 문서의 전체 높이


![그림 1-1](/assets/img/web/2021-03-22/1-11.png)

화면 높이: window.innerHeight

![그림 1-1](/assets/img/web/2021-03-22/1-10.png)
출처:https://sometimes-n.tistory.com/22