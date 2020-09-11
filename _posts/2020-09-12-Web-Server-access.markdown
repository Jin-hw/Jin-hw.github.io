---
layout: post
title:  "[EC2] Windows 웹서버 접속"
subtitle:   "EC2 windw"
categories: infra
tags: aws windows
comments: true
---

# 1.Windows 인스턴스로 원격 접속하는 방법  
---

 ![그림1-1](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-1.PNG)
원격 접속하고자 하는 인스턴스를 선택 후 오른쪽 클릭 후 [연결]을 누른다.  
  
 ![그림1-2](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-2.PNG)
[원격 데스크톱 파일 다운로드]를 클릭해서 파일을 다운 받는다. 그리고 다음으로 [암호 가져오기]버튼을 클릭한다.  
  
 ![그림1-3](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-3.PNG)
키 페어 경로 [파일 선택]을 클릭해서 자신의 비밀키 경로를 찾아서 선택한다.  
그리고 암호해독 버튼을 누른다.  
  
 ![그림1-4](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-4-1.png)
암호가 나타난다.  
  
 ![그림1-5](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-5-1.png)
아까 전에 다운 받은 원격 데스크톱 파일을 클릭한다.  
  
 ![그림1-6](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-4.PNG)
원격 데스크톱으로 로그인하는 창이 뜨면 암호를 입력한다.  
  
 ![그림1-7](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-5.png)
예를 눌러 원격 데스크톱에 접속한다.  
  
 ![그림1-8](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-6.PNG)
원격 데스크톱에 접속할 수 있음을 확인할 수 있다.  
  
# 2.원격 데스크톱에서 웹서버를 생성해 접속해보자  
---
 ![그림1-9](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-7.PNG)
우선 Server Manager에 접속한다.  
  
 ![그림1-10](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-8.PNG)
상단의 Manage를 클릭해서 [Add Roles and Features]를 클릭한다.  
  
 ![그림1-11](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-9.PNG)
쭉 Next를 누르다가 좌측의 Server Roles에서 멈춰서 Web Server (IIS)를 클릭한다.  
  
 ![그림1-12](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-10.PNG)
[Add Features]를 누른다.  
그리고 Next를 눌러 Install 한다.  
  
 ![그림1-13](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-11.PNG)
IIS를 설치한다.  
  
 ![그림1-14](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-12.PNG)
설치한 IIS를 검색해서 찾는다.  
  
 ![그림1-15](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-13.PNG)
좌측의 탭에서 EC2…을 클릭하고 Sites에 들어가서 Default Web Site를 오른쪽 클릭해서 explore를 클릭한다.

 ![그림1-16](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-14.PNG)
다음과 같은 창이 뜬다.  
  
 ![그림1-17](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-15.PNG)
메모장을 켜고 ‘Hello AWS’라는 문구를 적고 C:/inetpub/wwwroot에 index.html이라는 이름으로 파일을 저장한다.  
  
 ![그림1-18](http://jin-hw.github.io/assets/img/aws/2020-09-11-1/1-16.PNG)
외부 데스크톱에서 원격 데스크톱의 웹서버에 접속하면 원격 데스크톱의 IIS가 대응하는 것을 확인할 수 있다.