---
layout: post
title:  "[CodeDeploy] 현재위치 배포 실습"
subtitle:   "CodeDeploy in place"
categories: infra
tags: aws CodeDeploy
comments: true
---

# CodeDeploy로 In Place 배포
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-1.PNG)
IAM을 검색한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-2.PNG)
좌측 메뉴에서 [역할]을 클릭한 후 [역할 만들기]를 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-3.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-4.PNG)
[AWS 서비스]->[CodeDeploy]를 순차적으로 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-5.PNG)
[AWSCodeDeployRole]을 클릭해서 어떤 정책이 포함되어 있는지 확인이 가능한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-6.PNG)
역할 이름을 입력후 역할 만들기 버튼을 클릭해서 CodeDeploy를 위한 역할을 생성한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-7.PNG)
정책을 생성해 EC2 인스턴스를 역할을 정해야한다. 좌측 메뉴에서 [정책]-[정책 생성]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-8.PNG)
그림과 같은 JSON코드를 입력해서 정책을 설정해준다. 내용은 S3의 읽기 권한을 부여하는 것이라는 것을 알 수 있는데, 설정을 완료 후 코드로는 포함되지 않는 설정이 하나 있어서 별도로 설정을 해주어야한다.  
(CodeDeploy Agent가 S3에서 업로드된 파일을 가져오기 때문에 읽기 권한이 필요하다.)  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-9.PNG)
정책 검토 단계에서 그림과 같이 입력해준다.  
그리고 요약 부분에서 허용(1/239)옆의 '나머지 238'이라는 글자를 클릭해서 읽기 목록에서 제외된 하나의 항목을 클릭해서 엑세스 레벨 읽기가 전체허용이 되도록 해줘야한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-10.PNG)
IAM화면에서 [역할]-[역할 만들기]를 클릭한다.  
이는 생성한 정책을 적용하기 위함이다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-11.PNG)
[AWS 서비스] - [EC2]를 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-12.PNG)
이전에 생성한 정책인 exercise-code-deploy-ec2-policy를 검색해서 선택한다. 그리고 생성한다.   
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-13.PNG)
그림과 같이 생성을 완료한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-14.PNG)
다음은 배포가능한 인스턴스를 생성하기 위해 EC2를 검색한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-15.PNG)
그리고 이전에 중지 시켜둔 인스턴스를 다시 실행상태로 되돌린다.  
(인스턴스를 Auto Scailing을 통해서 CodeDeploy Agent를 설치해줘야하기 때문에)  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-16.PNG)
PuTTY를 통해서 인스턴스에 접속한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-17.PNG)
```git
	$ cd /sub/Mypro/
	$ rm -rf aws-exercise-*
#CodeDeploy는 자신이 배포할 디렉터리에 파일이 있은 경우 에러상황이라고 인식하기 떄문에 삭제해야한다.  
	
	$ wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install
	$ chmod +x ./install
	$ sudo ./install auto
	$ sudo service codedeploy-agent status
	$ sudo shutdown -h now
```
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-8.PNG)
인스턴스가 '중지' 된 것을 확인하고 이미지 생성을 한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-19.PNG)
위의 그림과 같이 설정한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-20.PNG)
이미지를 생성 후 위 그림과 같이 이미지가 생성된 것을 확인한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-21.PNG)
방금 생성한 이미지를 사용하기 위해서 시작 템플릿을 만들자  
좌측 메뉴에서 [시작템플릿]->[시작 템플릿 생성]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-22.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-23.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-24.PNG)
설정은 위의 그림과 같이 해준다.  


  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-25.PNG)
좌측 메뉴에서 [Auto Scailing Groups]-[편집]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-26.PNG)
추가 요금 발생 예방을 위해 설정했던 0,0,0 설정을 3,3,3 설정으로 바꾸어준다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-27.PNG)
좌측 메뉴 [인스턴스]를 클릭 후 추가 인스턴스가 3개 생성된 것을 확인한다.  


## CodeDeploy 애플리케이션 생성
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-28.PNG)
CodeDeploy를 검색 후 선택  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-29.PNG)
좌측 메뉴에서 [애플리케이션]->[애플리케이션 생성]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-30.PNG)
애플리케이션의 이름을 지정하고, EC2 인스턴스에 배포하는 방식으로 진행하므로 [EC2/온프레미스]를 선택해준다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-31.PNG)
그리고 배포그룹 생성을 클릭해서 배포그룹을 생성한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-32.PNG)
배포그룹 이름을 입력하고, 앞 부분에서 생성했던 정책을 적용하기 위해서 [exercise-code-deploy-service-role]을 선택해준다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-33.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-34.PNG)
나머지 설정은 그림과 같이 설정해주면 된다.   
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-35.PNG)
생성한 애플리케이션을 배포하기 위해 [배포 생성]을 클릭한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-36.PNG)
github를 통해 배포할 것이기 때문에 [애플리케이션을 github에 저장]을  선택한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-37.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-38.PNG)
로그인 한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-39.PNG)
배포하고자하는 리포지토리 이름을 입력하고 commit ID를 입력한다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-40.PNG)
그림과 같이 배포를 진행 중인것을 확인할 수 있다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-41.PNG)
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-42.PNG)
배포 완료가 되면 위와 같은 화면을 볼 수 있다.  

### 로드밸런서로 확인하기
---
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-43.PNG)
좌측 메뉴에서 [로드밸런서]를 선택하고, DNS 이름을 복사해서 브라우저로 접속해 본다.  
  ![그림 1-1](http://jin-hw.github.io/assets/img/aws/2020-09-16/1-44.PNG)
위 그림과 같이 배포가 정상적으로 작동함을 확인할 수 있다.   