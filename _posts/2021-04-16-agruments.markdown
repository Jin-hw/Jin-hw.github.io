---
layout: post
title:  "[Javascript] 가변 길이 인수 목록(Arguments 객체)"
subtitle:   "Arguments"
categories: develop
tags: front
comments: true
---

# 가변 길이 인수 목록(Arguments)
---
argument 변수는 모든 함수에서 사용할 수 있는 지역변수이다. 

또한, argument 변수의 값은 Arguments 객체이다.

함수의 인수를 지정한 것보가 넘겨서 호출하면 인수 값은 arguments에 저장된다.

ex) argument[0], ... arguments[n-1]


## Arguemnt 객체의 프로퍼티
---
argument.length: 인수의 개수
arugment.callee: 현재 실행되고 있는 함수의 참조

## 예시
---
```javascript
    function slashText(separator) {
        let s = "";
        for(let i=1; i < arguments.length, i++){
            s += separator[i];
            if( i< arguments.length-1) s+=separator;
        }
        return s;
    }
    console.log(slashText("/", "apple", "orange", "peach"));
    // -> apple/orange/peach
```

console.log()에서 인수를 slashText함수의 인수보다 많은 4개를 넣으면 첫번째 인수인 "/"를 제외하고는 모두 arguments객체에 들어가게 된다. 

즉, 

argument[1] = "apple", argumett[2] = "orange", argument[3] = peach 가 들어가게 된다.