---
layout: post
title:  "[Troubleshooting] React location 오류"
subtitle:   "React"
categories: develop
tags: front react troubleshooting
comments: true
---
# TypeError: Cannot read property 'location' of undefined 해결하기
---

![그림 1-1](/assets/img/web/troubleshooting/1-1.PNG)

위의 그림과 같이 에러가 발생하는 경우

![그림 1-1](/assets/img/web/troubleshooting/1-3.PNG)
위의 그림과 같이 
```
    import { Router } from "react-router-dom";
```
**Router**가 아닌 

```
    import { Route } from "react-router-dom";
```

**Route**이라고 적어주면 문제가 해결된다.