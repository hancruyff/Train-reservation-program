## 목차
[1. 개요](#1-개요)

[2. 주요 기능](#2-주요-기능)

[3. 데이터 베이스 설계](#3-데이터-베이스-설계)

[4. 보안](#4-보안)

## 1. 개요
기차예약 프로그램 개발

## 2. 주요-기능
로그인 기능

회원 가입 기능

관리자 메뉴
- 열차 관리
- 시간표 관리
- 가입 승인
- 회원 등급 변경

회원 메뉴
- 열차 예약
- 회원 정보 수정
- 예약 관리
- 시간표 조회
- 회원 탈퇴
  
<img src="https://github.com/user-attachments/assets/c94f6b4b-b321-467e-a67d-cd569675f1c1" width="500" height="294"/>

로그인 화면

<img src="https://github.com/user-attachments/assets/d02815d8-06de-4b4e-9995-4c1c11e78fa0" width="500" height="294"/>

회원 가입 화면
  
<img src="https://github.com/user-attachments/assets/36aa490a-d413-401d-81bd-de3ae582a06d" width="500" height="294"/>

관리자 메뉴 화면

<img src="https://github.com/user-attachments/assets/644f37ae-522b-4c91-befb-dcd8676f465e" width="500" height="294"/>

회원 메뉴 화면

<img src="https://github.com/user-attachments/assets/1279d04e-3c3e-4f4d-ad8b-6df6bce392fe" width="500" height="294"/>

예매 화면


## 3. 데이터 베이스 설계
<img src="https://github.com/user-attachments/assets/542b55de-bce4-4db8-86ee-982550ebbc07" width="300" height="119"/>

총 5개의 테이블로 구성

<img src="https://github.com/user-attachments/assets/163f57f4-4c38-494b-95b6-6199efc2901f" width="541" height="286"/>

회원 테이블과 열차좌석 테이블 간의 관계를 통해 참조 무결성을 유지

Foreign Key:
열차좌석 테이블의 회원번호 컬럼은 회원 테이블의 회원번호 컬럼을 참조하는 Foreign Key로 설정되어, 

데이터 무결성을 보장

## 4. 보안

SHA-256 방식을 이용하여 회원의 개인정보를 관리
