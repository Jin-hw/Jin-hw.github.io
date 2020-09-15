---
layout: post
title:  "[EC2] 로드 밸런싱 실습"
subtitle:   "EC2 Load Balancing"
categories: infra
tags: aws LoadBalancing
comments: true
---

# 로드 밸런싱 (Load Balancing)
---
로드밸런싱은 로드를 분산하는 기능이다.  
예를들어, 하나의 인터넷 회선을 이용한 인터넷 접속 대신 두 개의 인터넷 회선을 사용하는 것. 이렇게 되면 데이터가 두 라인 중 하나를 선택해서 이용하기 때문에 로드가 분산되는 효과를 얻을 수 있다. 
AWS에서는 로드 밸런서의 기능을 하는 서버를 내부적으로 관리를 한다. 따라서 로드 밸런서는 많은 데이터를 처리하고 있거나 정상적인 동작을 하지 않고 있는 서버로는 요청을 보내지 않는다.  


## 로드 밸런서 구성  
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-1.PNG)
로드밸런싱 메뉴에서 로드밸런서 생성을 클릭해 생성한다.  

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-2.PNG)
1. Step 1. 이번 실습은 HTTP를 통해서 이루어지므로 HTTP 생성을 클릭한다.  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-3.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-4.PNG)
로드 밸런서의 이름과 프로토콜을 그림과 같이 설정한다.  
2. Step 2. VPC도 a,c 두 가지를 설정한다.  

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-5.PNG)
3. Step 3. 보안 그룹은 제일 처음 생성한 인스턴스와 같은 보안그룹으로 설정한다.  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-6.PNG)
4. Step 4. 라우팅 대상 그룹의 이름과 경로를 설정한다.  

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-7.PNG)
5. Step 5. Auto Scailing에 의해 자동 등록되므로 따로 인스턴스를 설정할 필요는 없다.  

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-8.PNG)
로드 밸런서 생성완료  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-9.PNG)
좌측 메뉴에서 Auto Scailing - Auto Scailing 그룹을 클릭한다. 그리고 이름인 EXERCISE-GROUP을 클릭한다. 세부정보 탭에서 하단으로 스크롤을 내리면 그림과 같이 로드밸런싱이라는 항목 나온다. [편집]을 클릭한다.  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-10.PNG)
로드밸런서의 대상 그룹에서 방금 생성한 타겟 그룹의 이름을 선택한다.  그 후, 저장을 한다.

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-11.PNG)
좌측 메뉴에서 [로드 밸런싱] - [대상 그룹] 메뉴를 선택한 뒤 생성 타겟 이름인 exercise-target-group을 클릭해 인스턴스가 올바르게 등록된 것을 확인한다.  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-12.PNG)
좌측 메뉴에서 로드밸런싱 - 로드밸런서를 클릭한 뒤 생성한 exercise-lb를 클릭한다.  
그리고 DNS 이름을 복사한다.

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-15/1-1.PNG)
로드밸런서를 통해 애플리케이션이 올바르게 작동한 것을 확인할 수 있다.