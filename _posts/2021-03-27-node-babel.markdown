---
layout: post
title:  "[Troubleshooting] Node.JS Babel 설정"
subtitle:   "NodeJS"
categories: develop
tags: back node
comments: true
---

# Babel이란?
---
기존의 자바스트립트에서 모던 자바스크립트(ES6)를 사용할 수 있게 하는 방법

사용자가 모던 자바스크립트를 작성하면 예전의 자바스크립트 모양으로 변환해 줌

# Babel을 설치하는 방법
---
* 커맨드 라인 입력:
npm install @babel/node
* 커맨드 라인 입력:
npm install @babel/core
* 커맨드 라인 입력:
npm install @babel/preset-env
* 커맨드 라인 입력:
npm install core-js@3
* .babelrc 파일을 만들어주세요
* .babelrc 파일에 아래 내용을 입력 후 저장해주세요:
  
```json
    {
        "presets": [
            [
                "@babel/preset-env",
                    {
                        "useBuiltIns": "entry",
                        "corejs":3
                    }
            ]   
        ]
    }
```
* "package.json 파일"에서 스크립트로 작성해둔 start 에서 "node"를 "babel-node"로 바꿔주세요.
예) "start": "babel-node index.js"
* index.js 파일에 써뒀던 "const express" 라인을 지우시고 아래와 같이 바꿔주세요:
import "core-js";
import express from "express";
* 아래의 명령어를 커맨드 라인에 입력 후 실행, 테스트 해주세요:
npm start


자세한 내용은 이곳을 참고하시면 돼요: https://babeljs.io/docs/en/babel-preset-env