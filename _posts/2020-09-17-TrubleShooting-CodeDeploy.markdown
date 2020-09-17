---
layout: post
title:  "CodeDeploy TroubleShooting"
subtitle:   "CodeDeploy"
categories: infra
tags: codedeploy
comments: true
---

# CodeDeploy Throuble Shooting
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-17/1-1.PNG)
The overall deployment failed because too many individual instances failed deployment, too few healthy instances are available for deployment, or some instances in your deployment group are experiencing problems.  
애플리케이션을 통해서 배포를 위와 같은 에러가 발생할 수 있다.  

이 경우 두 해결방법은 두 가지를 생각해볼 수 있다. (이 두 가지 방법을 통해서 해결했기 때문에...)  
1. Auto Scailing 배포 그룹의 인스턴스에 CodeDeploy Agent가 설치되지 않았다.  
2. 정책 생성 시 읽기의 엑세스 레벨이 '전체'가 아닌 '제한' 일 경우  

## 배포그룹에 CodeDeploy Agent 설치
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-15.PNG)
기본 인스턴스 상태를 '실행 중' 상태로 만든다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-16.PNG)
Putty를 통해서 인스턴스에 접속한다.  
그리고 rm 명령어를 사용해서 codedeploy로 배포하기 위해서는 다른 파일이 존재하면 안되기 때문에 배포 경로에 있는 다른 파일들을 rm 명령어를 사용해서 삭제해준다.  
```git
		$ wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install
	$ chmod +x ./install
	$ sudo ./install auto
	$ sudo service codedeploy-agent status
	$ sudo shutdown -h now
```
위의 명령어를 통해서 Auto Scailing에 의해 복사되는 원본 인스턴스에 CodeDeploy Agent를 설치한다.  
이후에는 이미지 생성과 시작템플릿을 통해서 진행해주면 된다.  

## 정책 생성 시 읽기의 액세스 레벨을 전체로 설정하기
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-9.PNG)
위 그림과 같이 제한된 목록에 읽기가 들어가 있을 경우를 생각해 볼 수 있다.  
서비스 항목에 있는 [S3]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-17/1-2.PNG)
[정책편집]을 누른다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-17/1-3.PNG)
시각적 편집기에서 파란색으로 표시된 부분을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-17/1-4.PNG)
읽기를 체크해서 전체 액세스가 가능하도록 설정해준다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-17/1-5.PNG)
위 그림과 같이 읽기의 액세스 레벨이 전체로 변경된 것을 확인할 수 있다.
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-41.PNG)
다시 배포를 시도해보면 오류 없이 잘 배포되는 것을 확인할 수 있다.