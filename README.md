# 🚆 기차 예매 프로그램
### **C#과 Windows Forms를 활용한 GUI 기반 기차 예약 애플리케이션**

> 사용자가 기차를 선택하고, 날짜와 좌석을 예약할 수 있는 데스크톱 애플리케이션입니다.  
> 다중 폼 기반으로 설계되었으며, 예약 프로세스와 UI 전환이 직관적으로 구현되어 있습니다.

---

## 🗂 목차
- [1. 개요](#1-개요)
- [2. 주요 기능](#2-주요-기능)
- [3. 실행 화면](#3-실행-화면)
- [4. 실행 방법](#4-실행-방법)
- [5. 기술 스택](#5-기술-스택)
- [6. 프로젝트 구조](#6-프로젝트-구조)
- [7. 기여도 및 학습 내용](#7-기여도-및-학습-내용)

---

## 1. 📌 개요

이 프로젝트는 C#과 Windows Forms를 활용해 제작된 **기차표 예매 프로그램**입니다.  
사용자는 열차를 선택하고, 날짜, 시간, 좌석을 지정한 뒤 예매 완료까지 진행할 수 있습니다.

- 💻 **다중 폼 기반 UI**: 각 단계별로 Form1~Form6으로 구성
- 🎫 **예매 프로세스 구현**: 기차 선택 → 좌석 지정 → 예매 완료
- 📋 **데이터 흐름 관리**: 폼 간 정보 전달 및 상태 유지

---

## 2. 🧩 주요 기능

| 기능                     | 설명                                                                 |
|--------------------------|----------------------------------------------------------------------|
| 🚄 기차 목록 출력         | 사용 가능한 열차 리스트 제공 (Form1)                                  |
| 📆 날짜 및 시간 선택      | 승차일 선택 및 열차별 시간 설정 (Form2)                              |
| 💺 좌석 선택 인터페이스   | 좌석 시각화 및 클릭 기반 선택 구현 (Form3)                          |
| 🧾 예매 정보 요약 및 확인 | 사용자 입력 정보 종합 후 확인 화면 출력 (Form4)                      |
| 📩 예매 완료 처리         | 완료 메시지 표시 및 프로그램 종료 또는 재시작 옵션 제공 (Form5, Form6) |

---

## 3. 🛠 기술 스택

<img src="https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white"/>
<img src="https://img.shields.io/badge/.NET_Framework-512BD4?style=for-the-badge&logo=dotnet&logoColor=white"/>
<img src="https://img.shields.io/badge/Windows_Forms-0078D7?style=for-the-badge&logo=windows&logoColor=white"/>

- **C#**: 주요 로직 및 폼 제어 구현
- **.NET Framework (WinForms)**: UI 구성 및 이벤트 핸들링
- **Form Designer**: UI 시각 설계 도구
- **Visual Studio**: 전체 프로젝트 개발 및 디버깅 환경

---

### 4.🔗 데이터베이스 연결 및 CRUD 구현

프로그램은 SQLite를 사용하여 데이터베이스와 상호작용합니다. 이를 위해 System.Data.SQLite 라이브러리를 활용하며, 주요 기능으로는 데이터 조회(SELECT), 삽입(INSERT), 수정(UPDATE), 삭제(DELETE)가 있습니다.

### 4-1. 데이터베이스 연결 설정

```C#
using System.Data.SQLite;

string connectionString = "Data Source=TrainReservationDB.sqlite;Version=3;";
using (SQLiteConnection connection = new SQLiteConnection(connectionString))
{
    connection.Open();
    // 데이터베이스 작업 수행
}
```

### 🧾 4-2. 주요 테이블 SQL 예시

```sql
CREATE TABLE 열차 (
    열차ID INTEGER PRIMARY KEY AUTOINCREMENT,
    열차이름 TEXT NOT NULL,
    출발지 TEXT,
    도착지 TEXT
);

CREATE TABLE 운행시간표 (
    시간표ID INTEGER PRIMARY KEY AUTOINCREMENT,
    열차ID INTEGER,
    날짜 TEXT,
    시간 TEXT,
    FOREIGN KEY (열차ID) REFERENCES 열차(열차ID)
);

CREATE TABLE 좌석 (
    좌석ID INTEGER PRIMARY KEY AUTOINCREMENT,
    시간표ID INTEGER,
    좌석번호 TEXT,
    예약됨 INTEGER DEFAULT 0,
    FOREIGN KEY (시간표ID) REFERENCES 운행시간표(시간표ID)
);

CREATE TABLE 예매정보 (
    예매ID INTEGER PRIMARY KEY AUTOINCREMENT,
    이름 TEXT,
    연락처 TEXT,
    열차ID INTEGER,
    시간표ID INTEGER,
    좌석ID INTEGER,
    예매일시 DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (열차ID) REFERENCES 열차(열차ID),
    FOREIGN KEY (시간표ID) REFERENCES 운행시간표(시간표ID),
    FOREIGN KEY (좌석ID) REFERENCES 좌석(좌석ID)
);
```
---

### 4-3 데이터 흐름 & ERD
## 🔗 테이블 관계 (1:N 관계)

- `열차`  
  ↳ `운행시간표`  
  ↳ `좌석`  
   ↳ `예매정보`

각 테이블은 다음과 같은 방식으로 외래키(FK)로 연결됩니다:

| 부모 테이블 | 자식 테이블   | 관계 유형 |
|-------------|---------------|-----------|
| 열차        | 운행시간표     | 1 : N     |
| 운행시간표  | 좌석           | 1 : N     |
| 좌석        | 예매정보       | 1 : 1 또는 1 : N |

### ▶️ 예매 흐름

사용자가 열차를 선택

→ 해당 운행시간표를 선택

→ 좌석을 선택

→ 예매정보에 모든 선택 정보를 통합하여 저장


## 5. 🖼 실행 화면
<img src="https://github.com/user-attachments/assets/c94f6b4b-b321-467e-a67d-cd569675f1c1" width="500" height="294"/>
<img src="https://github.com/user-attachments/assets/d02815d8-06de-4b4e-9995-4c1c11e78fa0" width="500" height="294"/>
<img src="https://github.com/user-attachments/assets/36aa490a-d413-401d-81bd-de3ae582a06d" width="500" height="294"/>
<img src="https://github.com/user-attachments/assets/644f37ae-522b-4c91-befb-dcd8676f465e" width="500" height="294"/>
<img src="https://github.com/user-attachments/assets/1279d04e-3c3e-4f4d-ad8b-6df6bce392fe" width="500" height="294"/>

---

## 6. ▶ 실행 방법

### ✅ 실행 절차

1. Visual Studio에서 `.sln` 파일 열기  
   - `WindowsFormsApp1.sln` 클릭

2. 상단 툴바에서 ▶ (디버그 실행) 클릭  
   또는 `Ctrl + F5`로 실행

3. 프로그램 실행 후 다음 순서대로 진행  
   - 기차 선택 → 날짜/시간 → 좌석 선택 → 정보 확인 → 예매 완료

---

## 7. 📁 프로젝트 구조
```
WindowsFormsApp1/
├── Form1.cs / Form1.Designer.cs / Form1.resx   → 기차 선택
├── Form2.cs                                     → 날짜 및 시간 선택
├── Form3.cs                                     → 좌석 선택
├── Form4.cs                                     → 예매 정보 확인
├── Form5.cs, Form6.cs                           → 예매 완료 및 종료
├── Program.cs                                   → 앱 진입점
└── WindowsFormsApp1.sln                         → 솔루션 파일
```

---

## 7. 🧑‍💻 기여도 및 학습 내용

✔️ 폼 간 데이터 전달 (Constructor 또는 Static 활용)  
✔️ 이벤트 기반 프로그래밍 및 WinForms 라이프사이클 이해  
✔️ 좌석 선택 구현을 위한 컨트롤 동적 배치 및 색상 제어  
✔️ 사용자 경험(UX) 흐름 설계 및 전환 타이밍 구현  
✔️ 상태 관리 없이 단계별 흐름 제어하는 간결한 UI 모델 학습  
