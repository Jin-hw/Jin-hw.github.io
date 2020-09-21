---
layout: post
title:  "[Lightsail] 홈페이지 만들기(Wordpress) "
subtitle:   "Lightsail"
categories: infra
tags: lightsail wordpress
comments: true
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/AWS lightsail logo.jpeg)

# Lightsail 이란?
---
Lightsail은 몇번의 클릭만으로 가장 간단하게 AWS의 간편함을 실감할 수 있는 서비스이다. 그 이유는 클라우드 아키텍처의 네트워크 단계부터 애플리케이션 단계까지 모든 것을 제공해주기 때문에 별도의 설정과 관리가 불필요하기 때문이다.  따라서 몇번의 클릭만으로 미리 구성된 애플리케이션(WordPress, Magento, Plesk, Joomla 등)을 통해 몇 분안에 AWS서비스를 사용할 수 있다. 
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/2-1.PNG) 


## Lightsail의 요금 정책
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/2-2.PNG)
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/2-3.PNG)  
위의 그림과 같은 타 서비스의 100개가 넘는 요금 정책에 비해 심플한 요금체계를 가지고 있다.  
처음 사용하는 사용자는 가장 낮은 단계인 3.50USD 서비스를 한달간 무료로 사용할 수 있다. 하지만 이는 시간적인 한달(750시간)이기 때문에 주의할 필요가 있다. 만약 인스턴스를 2개를 만들어서 사용하면 사용시간은 2배가 되고, 인스턴스를 3개를 사용하면 사용시간은 3배가 되므로 인스턴스를 3개 사용하게 되면 250시간 밖에 사용할 수 없다는 것이 된다.

## Lightsail 블로그 만들기(Wordpress 사용)
---

### Step 1. 콘솔에 접속
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-0.PNG)
[AWS 홈페이지](https://aws.amazon.com/)에 접속한다. 그리고 [콘솔에 로그인]을 클릭해서 로그인을 한다.    

### Step 2. Lightsail 선택
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-1.PNG)
콘솔에 로그인을 한 뒤 [솔루션 구축] 탭에서 [Lightsail을 사용하여 가상 서버 구축]을 선택한다.  


### Step 3. Lightsail 언어 선택
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-2.PNG)
자신이 사용할 언어를 설정하고 save를 한다.  

### Step 4. 인스턴스 생성
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-3.PNG)
위 과정을 따라왔다면 인스턴스 이미지 선택하는 과정에 왔을 것이다. 이 단계에서는 **플랫폼**과 **블루프린트**를 선택할 수 있다. **플랫폼**에서는 자신이 사용할 운영체제를, **블루프린트**에서는 자신이 사용할 애플리케이션을 선택한다.  
* 플랫폼: Linux/Unix  
* 블루프린트: WordPress 를 현재 실습에서 사용하기 위해 선택해준다.  

### Step 5. 인스턴스 플랜 선택
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-4.PNG)
**인스턴스 플랜 선택**에서는 월별 요금을 선택할 수 있다. 실습에서는 최소한의 사양만을 필요로하기 때문에 한 달 무료로 사용할 수 있는 $3.5 요금을 선택하도록 한다.  
(위의 [Lightsail의 요금 정책](#Lightsail의-요금-정책)에서 언급한대로 여러대의 인스턴스를 사용하면 사용시간이 배로 줄어들기 때문에 주의가 필요하다. )  
**인스턴스 확인**에서 리소스의 이름의 오른쪽에 있는 숫자를 늘리면 수 만큼의 가상서버가 생성된다. (추가 비용이 발생하니 주의)  

### Step 6. Lightsail 인스턴스 생성 확인
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-14.PNG)
설정을 마치면 위와 같이 인스턴스가 생성된다. (생성 중이라는 글씨가 보인다면 잠시 기다리면 완료된다.)  
그리고 IP주소를 복사해서 브라우저에 붙여넣기 해서 생성된 워드프레스에 접속한다.  

### Step 7. WordPress 접속확인
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-5.PNG)
IP주소를 복사해서 접속하면 위와 같은 "Hello Word"가 적힌 화면이 뜬다. 만약 바로 뜨지 않는다면 조금 기다렸다가 새로고침을 하면 접속이 된다.  

### Step 8. WordPress 관리자 접속
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-6.PNG)
생성된 워드프레스를 수정하기 위해서는 관리자 화면에 접속해야한다. 관리자 화면에 접속하기 위해서는 브라우저 상단의 주소창에서 IP주소의 뒷부분에 /wp-admin 이라고 적고 엔터를 치면 위와 같은 화면에 접속이 된다. 하지만 현재의 상태로는 관리자 ID와 Password를 모르기 때문에 별도의 작업이 필요하다.  

### Step 9. WordPress 관리자 ID와 Password
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-7.PNG)
[라이트세일의 대시보드](https://lightsail.aws.amazon.com/ls/webapp/home/instances) 로 가면 위와 같은 그림의 화면이 보인다. 그리고 형광편으로 표시된 부분을 클릭해준다.  
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-8.PNG)
그러면 위와 같은 CLI(Command Line Interface)환경의 창이 팝업창으로 나타나게 된다.  
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-9.PNG)
```git 
	$ cat bitnami_credentials
```
라는 명령어를 입력하면 위 그림과 같은 화면이 나타나고 노란색 형광팬으로 표시된 부분에 관리자 ID와 Password가 표시된다.  

### Step 10. 관리자 로그인
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-10.PNG)
다시 WordPress 로그인 화면으로 돌아온다. 그리고 Step 9에서 확인한 ID와 Password를 입력해서 로그인한다.  
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-11.PNG)
위와 같은 관리자 화면으로 접속되는 것을 확인할 수 있다.  

### Step 11. WordPress의 기본 언어 바꾸기
---
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-12.PNG)
관리자 화면에서 좌측 메뉴의 [Setting]이라는 메뉴를 클릭한다.  
그리고 Site Language라는 설정에서 자신에게 편한 언어를 설정할 수 있다.  
 ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-20/1-13.PNG)
한국어로 설정하면 기존의 영어였던 페이지의 기본 설정이 한국어로 바뀐 것을 확인할 수 있다.