---
layout: post
title: Binary Log를 이용하여 파이썬에서 Azure Database for MySQL 데이터 변경 정보를 가져오기
date: 2024-04-27 21:56:23 +0900
category: sample
---

이번 포스팅의 목적은 Azure Database for MySQL 서버에서의 CRUD작업에 대해 데이터를 캡처해 Microsoft Fabric의 Warehouse에 변경사항을 적용할 수 있는지에 대한 테스트입니다.

# 1. Azure Database for MySQL 설치하기
테스트를 위해 Azure Database For MySQL 서버를 설치합니다.

1. Azure 포탈로 이동하여 상단의 '리소스 만들기'를 클릭합니다.  
![리소스 생성 화면 1](/public/img/20240427-mysql-binlog/image1.png)


1. 'mysql'을 검색하여 표시되는 'Azure Database for MySQL'을 Create합니다.  
![리소스 생성 화면 2](/public/img/20240427-mysql-binlog/image2.png)


1. '유연한 서버'를 선택합니다.  
![리소스 생성 화면 3](/public/img/20240427-mysql-binlog/image3.png)


1. 아래와 같이 입력 후 '검토+만들기'를 누릅니다.  
    - 구독 및 리소스 그룹 - 리소스를 생성할 구독 및 리소스그룹을 선택합니다.
    - 서버 이름 - 사용할 서버 이름을 입력합니다.
    - 지역 - Korea Central
    - MySQL 버전 - 8.0
    - 워크로드 유형 - 개발 또는 취미 프로젝트용
    - 가용성 영역 - '기본 설정 없음'
    - 인증 방법 - 'MySQL 인증만'
    - 관리자 사용자 이름, 비밀번호 - 관리자 계정 정보로 사용을 원하는 계정 및 패스워드 입력
![리소스 생성 화면 4](/public/img/20240427-mysql-binlog/image4.png)
![리소스 생성 화면 5](/public/img/20240427-mysql-binlog/image5.png)

# 2. 테이블 생성

# 3. Fabric Notebook에 파이썬 코드 작성


This is code
```ruby
print 'hello world'
```