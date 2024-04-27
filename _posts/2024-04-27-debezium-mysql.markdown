---
layout: post
title: Binary Log를 이용하여 파이썬에서 Azure Database for MySQL 데이터 변경 정보를 가져오기
date: 2024-04-27 21:56:23 +0900
category: sample
---

이번 포스팅의 목적은 Azure Database for MySQL 서버에서의 CRUD작업에 대해 데이터를 캡처해 Microsoft Fabric의 Warehouse에 변경사항을 적용할 수 있는지에 대한 테스트입니다.

# 1. Azure Database for MySQL 설치하기
테스트를 위해 Azure Database For MySQL 서버를 설치합니다.
  
1. **Azure 포탈로 이동하여 상단의 '리소스 만들기'를 클릭합니다.**  
![리소스 생성 화면 1](/public/img/20240427-mysql-binlog/image1.png) 
<!-- # {: width="1200" height="400"} -->
  
  
1. **'mysql'을 검색하여 표시되는 'Azure Database for MySQL'을 Create합니다.**  
![리소스 생성 화면 2](/public/img/20240427-mysql-binlog/image2.png){: width="70%" height="70%"} 
  
  
1. **'유연한 서버'를 선택합니다.**  
![리소스 생성 화면 3](/public/img/20240427-mysql-binlog/image3.png){: width="50%" height="50%"}


1. **아래와 같이 입력 후 '검토+만들기'를 누릅니다.**  
    - 구독 및 리소스 그룹 - 리소스를 생성할 구독 및 리소스그룹을 선택합니다.
    - 서버 이름 - 사용할 서버 이름을 입력합니다.
    - 지역 - Korea Central
    - MySQL 버전 - 8.0
    - 워크로드 유형 - 개발 또는 취미 프로젝트용
    - 가용성 영역 - '기본 설정 없음'
    - 인증 방법 - 'MySQL 인증만'
    - 관리자 사용자 이름, 비밀번호 - 관리자 계정 정보로 사용을 원하는 계정 및 패스워드 입력
![리소스 생성 화면 4](/public/img/20240427-mysql-binlog/image4.png){: width="70%" height="70%"}
![리소스 생성 화면 5](/public/img/20240427-mysql-binlog/image5.png){: width="70%" height="70%"}

  
1. **생성이 완료되었다면 리소스로 이동합니다.**  
![리소스 생성 화면 6](/public/img/20240427-mysql-binlog/image6.png){: width="70%" height="70%"}
  
  
1. **리소스로 이동하였으면 좌측 메뉴의 '데이터베이스'를 선택합니다.**  
![리소스 생성 화면 7](/public/img/20240427-mysql-binlog/image7.png){: width="30%" height="30%"}
  
  
1. **'+추가' 버튼을 선택합니다.**  
![리소스 생성 화면 8](/public/img/20240427-mysql-binlog/image8.png){: width="70%" height="70%"}
  
  
1. **데이터베이스 만들기 화면에서 생성할 데이터베이스 이름 입력 후 저장 버튼을 누릅니다.**
![리소스 생성 화면 9](/public/img/20240427-mysql-binlog/image9.png){: width="70%" height="70%"}


테스트를 위한 MySQL 서버 생성을 완료하였습니다. 이미 테스트를 위한 MySQL 환경이 구성되어 있는 상태라면, 위의 과정을 생략해도 좋습니다.
다음은, 생성한 MySQL Server에 DBeaver를 사용해 접근하여 데이터베이스에 테이블을 생성하고 Insert, Update, Delete 등의 CRUD 작업을 수행하는 방법을 알아보겠습니다.
# 2. 테이블 생성

# 3. Fabric Notebook에 파이썬 코드 작성

