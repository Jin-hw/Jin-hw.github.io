---
layout: post
title:  "[EC2] 인스턴스 생성과 리눅스로 실행"
subtitle:   "EC2 instance"
categories: infra
tags: aws instance EC2
comments: true
---
  
  
## 인스턴스 생성  
---
### -Step 1: AMI 선택  
AMI는 쉽게 말해 운영체제를 선택하는 것  
 ![그림1-1](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-1.PNG)
Linux, Ubuntu, Windows 등 각종 운영체제를 지원한다.  
  
### -Step 2: 인스턴스 유형 선택  
 ![그림1-2](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-2.PNG)
사용할 인스턴스의 사양을 선택한다. (자신이 사용할 성능에 맞게 선택하는 것이 가장 중요)
프리티어가 적힌 기능만 1년간 무료로 사용가능 ([프리티어 EC2 요금 정책](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc))  
유형(Type):Large>Medium>Small>Micro>Nano  
유형 중 메모리 성능이 높은 것은 m, CPU의 성능이 높은 것은 c가 붙어있다.  
  
### -Step 3: 인스턴스 세부 정보 구성  
 ![그림1-6](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-6.png)
종료 방식: 만든 컴퓨터를 중지할 것인지 종료할 것인지 설정할 수 있다. 중지하면 사용하지 않을 때는 끄고 사용할 때는 켤 수 있어서 요금을 아낄 수 있다.  
  
### -Step 4: 스토리지 추가  
 ![그림1-7](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-7.PNG)
메모리 크기: 30GB 까지는 무료로 사용할 수 있다.  
볼륨 유형: SSD 타입과 마그네틱 타입을 설정할 수 있다.  
IOPS: 저장장치의 속도를 조정할 수 있다.  
종료 시 삭제: 현재 만드는 저장 장치는 인스턴스와는 분리된 저장장치이다. 체크를 하면 인스턴스 삭제 시 같이 삭제됨.  
  
### -Step 5: 태그 추가  
 ![그림1-8](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-8.PNG)
인스턴스를 만들고 해당 인스턴스의 정보를 저장할 수 있다. 환경에 따라 수백 개의 인스턴스를 사용하는 경우도 있다.  
  
### -Step 6: 보안 그룹 구성 
 ![그림1-9](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-9.PNG)
리눅스는 유형이 SSH로 지정되지만, 운영체제를 윈도우로 했다면 RDP로 지정된다.
웹서버로 사용하려면 HTTP를 추가하고 소스는 위치 무관으로 설정해서 80번 포트를 통해서 어떤 위치에서도 접속할 수 있도록 설정해야 한다  
  
### -Step 7: 인스턴스 시작 검토  
 ![그림1-10](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-10.PNG)
인스턴스를 생성하기 전에 현재까지의 설정을 확인할 수 있다. 제대로 입력이 되었다면 시작하기 버튼을 누른다.  
  
  
### -Step 8: 키 페어 생성
---
 ![그림1-11](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-11.PNG)
새 키 페어 생성을 선택하고 이름을 설정해준다-> 키페어 다운로드 버튼을 누르면 비밀번호가 파일로 저장된다. (주의: 키 페어를 발급 받으면 다시 발급되지 않음)  
  
### -Step 9: 인스턴스 생성완료
 ![그림1-12](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-12.PNG)
생성된 인스턴스(i-07f6440…)를 클릭  
  
 ![그림1-13](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-13.PNG)
생성 완료된 인스턴스를 확인할 수 있다. (인스턴스 상태가 ‘pending’인 상태라면 ‘running’상태가 될 때까지 기다린다.)  

# 윈도우에서 생성된 리눅스 서버로 접속하는 방법  
---
[XShell6 이용](https://www.netsarang.co.kr) 가정, 학생 무료  
  
 ![그림1-14](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-14.PNG)
생성된 인스턴스에서 오른쪽 마우스 클릭해서 연결 클릭  
  
 ![그림1-20](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-20.png)
드래그한 퍼블릭 DNS부분을 복사한다.   
  
 ![그림1-18](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-18.PNG)
XShell6을 실행하고 열기를 누른다. -> 호스트에 복사한 부분을 붙여넣는다.  
  
 ![그림1-19](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-19.PNG)
사용자 인증 탭을 누르고 방법(M)에서 Public Key를 설정한다. -> 사용자 키에서 키페어 다운로드한 파일을 선택한다. -> 연결한다.  
  
 ![그림1-15](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-15.PNG)
수락 및 저장을 눌러 연결을 완료한다.  

 ![그림1-16](https://jin-hw.github.io/assets/img/aws/2020-09-11/1-16.PNG)
리눅스에서 AWS EC2로 연결 완료된 것을 확인할 수 있다.

