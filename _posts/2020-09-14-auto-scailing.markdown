---
layout: post
title:  "[EC2] Auto Scailing 실습"
subtitle:   "EC2 autoscailing"
categories: infra
tags: aws Web autoscailing
comments: true
---

# Auto Scailing이란?
---
aws auto scailing이란 aws에서 제공하는 자동 다중 서버 서비스이다.   
같은 사양, 환경, 코드를 가진 EC2 인스턴스의 묶음이다.  
이 서비스는 서비스에 클라이언트가 많이 몰려드는 경우에 서버 수를 늘리고 클라이언트의 엑세스가 적을 때에는 서버의 수를 자동으로 줄인다. 따라서 지속적으로 여러 대의 서버를 운용하는 것보다 필요할 때 필요한 만큼의 수의 서버를 운용할 수 있기 때문에 효과적인 서비스 운영이 가능하다.  
  
# Auto Scailing 설정
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-1.PNG)
auto scailing 하고자 하는 인스턴스를 실행 중지 시킨다.  
그 다음 [이미지]에서 [이미지 생성]을 클릭한다.  

  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-2.PNG)
이미지 이름을 작성하고 이미지 생성을 클릭해서 새로운 이미지를 생성한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-3.PNG)
이미지 생성완료 화면  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-4.PNG)
다음은 [인스턴스]-[시작 템플릿]으로 들어가서 [시작 템플릿 생성] 버튼을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-5.PNG)
시작 템플릿의 이름과 버전 설명을 작성한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-6.PNG)
다음으로 AMI는 젤 처음에 생성했던 AMI ID를 적어서 검색한다.  
(좌측의 [이미지]-[AMI] 를 차례로 클릭하면 우측에서 생성한 이미지 정보를 확인할 수 있다. 거기서 AMI ID를 확인가능)  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-7.PNG)
네트워크 설정은 VPC로 하고 보안 그룹은 정지했던 인스턴스와 같은 보안그룹으로 설정한다.  
그리고 [시작 템플릿 생성]을 클릭해서 템플릿을 생성한다.    
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-8.PNG)
다음은 좌측의 [Auto Scailing] - [Auto scailing 그룹 생성]을 클릭한다.   
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-9.PNG)
시작 템플릿의 이름을 선택하고 다음으로 넘어간다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-10.PNG)
서브넷은 2a,2c 두 가지를 선택해준다. 이것은 생성하는 인스턴스들 중 절반은 서울 리전의 a가용 영역에서, 절반은 서울 리전의 c가용 영역에 생선한다는 것을 의미한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-1.PNG)
우리는 auto scailing을 실험해 보고자 하므로 최소 용량은 1, 최대 용량은 2로 설정한다.  
그 다음 하단의 조정 정책에서 [없음]이 아닌 [대상 추적 조정 정책]을 선택한다.  
그리고 대상 값을 80으로 설정한다. 이를 통해 auto scailing 그룹 내에서 CPU 사용률이 80%를 넘어 가면 인스턴스의 수가 최대 2대 까지 자동으로 변하는 것을 확인할 수 있다.  
생성을 완료한다.  
  
이제 인스턴스의 갯수가 자동으로 변하는 것을 확인해 보기 위해 EC2에 PuTTY로 접속을 한다.  
서버에 접속을 하고나서 stress 라는 애플리케이션을 설치한다. stress는 부하를 걸어서 원하는 시간만큼 CPU를 100% 사용하게 만드는 애플리케이션이다.  
```git
	$ sudo yum install stress -y

...
Complete!

	$ stress --cpu 1 --time 600
```
이라는 코드를 입력하면 10분 후에 생성한 이미지 EXERCISE-GROUP의 활동기록을 통해서 활동 기록을 확인할 수 있다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-14/1-12.PNG)
위의 그림과 같이 인스턴스가 처음에 생성되어 0->1개로, stress 애플리케이션에 의해서 인스턴스는 1->2개로 늘어났다가, 스트레서 애플리케이션 기능이 종료되고 나서 다시 2->1개로 돌아오는 것을 확인할 수 있다.  
이렇듯 AWS의 Auto Scailing 기능은 자동적으로 필요에 의해 인스턴스를 늘리고 줄여주므로 원활한 접속을 가능하게 한다.  