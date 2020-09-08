---
layout: post
title:  "리눅스 명령어(업데이트 중)"
subtitle:   "Linux"
categories: infra
tags: linux list
comments: true
---
## 주의사항
---
>명령어는 자기가 현재 위치한 디렉토리를 대상으로 작동한다.

## CLI(Commend Line Interface)
---
리눅스는 문자를 입력해서 명령을 한다.



## 명령어
---
 * pwd:현재 위치를 표시
 * mkdir(Make Directory): 디렉토리 생성 
 * ls: 파일과 디렉토리를 확인
 * ls -l,a(파라미터): 자세한 목록을 제공

 * drwx
 d: Directory(디렉토리)
 r : Read(읽기 권한) 
 w : Write (쓰기 권한)
 x : eXecute (실행 권한)

 * cd(Change Directory): 디렉토리의 위치를 바꿈
 * cd .. : 상위 디렉토리로 이동
 * clear: 터미널 창 정리
 * ?? --help: ??명령어에 해당되는 설명을 제공
 * rm [파일명]: 파일 삭제 (디렉토리는 삭제할 수 없음)
 * rm -r [디렉토리명]: 디렉토리 삭제

 * sudo(Super User Do): 권한이 필요한 명령어를 실행
 * top: 현재 컴퓨터에서 실행되고 있는 목록을 보여줌
 * apt-cache search [??]: ??에 관련된 모든 프로그램을 찾아줌
 * apt-get insall [??]: ??프로그램을 설치
 * apt-get upgrade [??]: ??프로그램을 업그레이드 함
 * apt-get remove [??]: ??프로그램을 제거함
 * wget [URL]: 온라인상의 파일을 다운 받음
 * git clone [URL] : 깃허브에 다른 사람이 올린 파일을 전부 다운 받음
 * cat [파일명] : 파일의 내용을 표시함
 * grep [검색어] [파일명]: 파일 속에서 검색하고 싶은 단어가 들어간 행을 찾아줌
