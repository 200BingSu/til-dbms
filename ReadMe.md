# 데이터베이스 모델링 및 ERD 및 MySQL 활용하기

- MySQL(DBMS 8.x): RDBMS를 다룬다(Relation:관계)

## 1. 요구사항 분석

- 회의 참석(회의록)
- 회의록 검토 후 각 사항을 요구 사항 분석(요구사항정의서, 업무 지시서)

## 2. 요구사항 분석 필요 이유

- Entity의 속성을 찾기
- 각 내용의 속성 찾고 분류
- 분류된 내용을 모아서 Entity로 생성
- Entity와 Entity 간 관계 찾기.
- 요구사항 정의서 작성

### 2.1. 요구사항 분석 예

- 고객은 고객코드 , 고객명 , 전화번호 , 이메일, 주소(기본주소 , 상세주소), 지역 , 가입일로 되어있다
- 고객은 지역별로 관리되도록 한다 .
- 지역은 지역코드와 지역명으로 되어 있고 지역명은 대한민국의 지역코드 (02:서울특별시)를 이용한다
- 한 지역에는 여려 고객이 있을 수 있다
- 제품은 제품코드 , 제품명 , 제품색상 , 가격으로 되어있다
- 하나의 제품은 여러 색상을 가질 수가 있다
- 고객은 등록된 제품을 구매 할 수 있다
- 한 명의 고객은 여러 제품을 구매 할 수 있고 , 하 나의 제품은 여러 고객이 구매 할 수 있다
- 고객이 제품을 구매 시 구매수량과 구매일자를 기록한다

### 2.2. 요구사항 정의서 또는 업무 기수서(회사마다 포맷이 다름)

![Image](https://github.com/user-attachments/assets/184f73e9-c187-4e88-bffc-99f52ae452b9)

### 2.3. 속성을 찾기 후 Entity 정의하기

- 데이터 베이스 설계 전문가는 Entity 정의 후 속성을 선별해 나간다.
- 신입 데이터 설계자는 Attribute 선별 후 Entity를 정의한다.

#### 2.3.1. 먼저 Entity 항목 정리

![Image](https://github.com/user-attachments/assets/0a50df9a-d2a1-4546-948c-0be215db4fb5)

#### 2.3.2. Entity와 Entity의 관계 정리

: 동사 소문자 추천
![Image](https://github.com/user-attachments/assets/d146a042-4ac5-41ce-991e-93365965ab98)

## 3. ERD 그리기

### 3.1. 개념적 모델링

- Entity-Relationship-Diagram
- E-R 다이어그램
  ![Image](https://github.com/user-attachments/assets/f90a4a43-e195-414e-92a4-820590f471a7)
- 고객
  ![Image](https://github.com/user-attachments/assets/fae0a3cf-b127-4ace-a2eb-a6274053899a)
- 고객 PK 후보
  ![Image](https://github.com/user-attachments/assets/0f80e6aa-08f0-4289-a1cc-ea01add592d2)
- 지역
  ![Image](https://github.com/user-attachments/assets/e12ae064-54dd-4716-984c-12613461c445)
- 제품
- ![Image](https://github.com/user-attachments/assets/50454635-4e5c-448f-8ff4-8eaf263b4b2a)

### 3.2. Relation 표현하기

![Image](https://github.com/user-attachments/assets/09e874f5-4dd9-4623-869c-6da5af2e26bc)

#### 고객은 제품을 구매한다

![Image](https://github.com/user-attachments/assets/3917cb62-b834-4e1e-8382-a0a4b84eb7c4)

#### 지역은 고객을 관리한다.

![Image](https://github.com/user-attachments/assets/5633836e-15b3-436c-b300-ec28bd157d2b)

## 4. Logical Data Modeling(논리적 모델링)

- 개념적 스키마를 표형식 또는 테이블 형식으로 표현한다.
- ENtity의 속성 데이터 타입, 길이, null 허용 여부, 기본값, 제약 조건 등을 세부적으로 작성 후 문서화
- 즉 `테이블 정의서`를 만든다. (도구 다양)
  ![Image](https://github.com/user-attachments/assets/9d7915e4-b238-41c3-a3f2-92ab82e62b71)

## MySQL 설치
- https://dev.mysql.com/downloads/installer/