# 데이터베이스 모델링

## 1. DB 즉 데이터 베이스와 DB 관리 시스템은 다른 개념이다.

- DB : 데이터를 저장하는 공간
- DB 관리 시스템 : DB를 관리하는 시스템

## 2. 데이터베이스 모델링

- 데이터베이스 모델링은 데이터베이스를 설계하는 과정이다.
- 데이터를 잘 분류해서 저장하는 방안을 고려하는 과정.
- 잘 분류해 두면 데이터를 쉽게 찾을 수 있고, 데이터를 쉽게 추가하고 삭제할 수 있다.

## 3. 데이터베이스 모델링에서 최종 목적

- 데이터의 중복을 제거한다.
- 데이터의 무결성을 보장한다.
- 데이터의 일관성을 보장한다.

## 4. 우리는 관계(relation)형태의 데이터베이스를 사용.

- RDBMS(관계형 데이터베이스 관리 시스템)
- 관계형 데이터베이스는 테이블(table)로 구성된다.
- 테이블은 행(row)과 열(column)로 구성된다.
- 행은 레코드(record)라고 부른다.
- 열은 필드(field)라고 부른다.
- MySQL, Oracle, MSSQL, PostgreSQL, MariaDB 등이 있다.

## 5. 모델링 과정

### 5.1. 요구사항 분석

- 서비스 기획 참석 이후
- 문장으로된 다양한 서비스 내용에 대해서 우선 대표적 속성(attribute)를 추출해 낸다.
- 추출된 속성(Attribute)을 이용해서 하나의 개체(Entity)로 분류한다.
- 개체 즉 Entity 간의 관계(relation)을 분석한다.
- 이러한 개체(Entity)들을 묶어서 하나의 스키다(schema)로 분류한다.

### 5.2. 개념적 데이터 모델링

- ERD: Entity Relation Diagram

### 5.3. 논리적 데이터 모델링

- Excel 활용 및 PK(Primary Key), FK(Foreign Key) 설정, Relation Moel 만들기

### 5.4. 물리적 데이터 모델링

- 테이블 정의서, SQL Script 최종 생성

### 5.5. 데이터베이스 구축

- Reverse Engineering
- Forwad Engineering

## 6. 데이터베이스 모델링 실습

### 6.1. 핵심 `중복되는 데이터 제거`

- Schema 생성하기
  : `소문자` 폴더로 저장
- Entity(객체)를 파일로 table 생성함
  : `복수형 명사` 파일로 저장
- 속성(Attribute) 생성함
  : `소문자` 칼럼 명을 생성함.
  - PK
    : 절대 중복되지 않는 조건
    : 자동 증가 또는 유니크 속성을 부여하여야 함.
    : 자동 증가는 auto increment 속성을 부여하여야 함.
    : 유니크 속성은 uuid 속성을 부여하여야 함.
  - FK
    : 외래키 속성을 부여하여야 함.
    : 다른 테이블 즉, 엔티티와 관계를 연결시키는 키다.
    : 일반적으로 다른 테이블의 PK가 연결된다.
    : 중복되는 데이터를 제거하기 위해 참조하는 속성
    : 참조하는 속성은 참조하는 속성의 칼럼 명을 부여하여야 함.
- 관계(Relation) 생성하기
  : `소문자` 파일로 저장

### 6.2. 핵심 `데이터의 내용은 1개여야 한다.`

- 레코드 즉 입력되어져 있는 데이터가 만약 여러개라면
  : 데이터를 하나씩 배치하여서 FK로 연결시켜본다.
  : 만약 FK가 여러개 배치된다면
  : 새로운 표를 생성해보고, 각 FK를 통해서 연결을 시켜보자.

### 6.3. 대응수 알아보기

- 꼭 엑셀을 만들지 않더라도 대응수를 파악할 수 있다.
- 대응수란 하나의 테이블이 다른 테이블의 FK 활용하는 것을 나타내는 기호다.
- `1:1` 구조
- `1:n` 구조
- `n:m` 구조

#### 대응수 알아내기 요령

- A와 B의 관계
- A는 B를 ~~ 한다.
- B는 A에 의해 ~~한다.
- `하나`의 A는 `한개/여러개`의 B를 ~한다.
- `하나`의 B는 `한개/여러개`에 의해 A를 ~한다.

#### 6.3.1. `1:n 구조`

- `회원`과 `이메일`의 관계를 파악해보자.
- 회원은 이메일을 가지고 있다.
- 이메일은 회원에게 소유되어 있다.
- 한명의 회원은 여러개의 이메일을 소유하고 있다.
- 하나의 이메일은 한명의 회원에게 소유되어 있다.
- 최종적으로 회원:이메일은 `1:n`이다.

#### 6.3.2. `n:M 구조`

- `학생`과 `과목`의 관계를 파악해보자.
- 학생은 과목을 수강한다.
- 과목은 학생에 의해 수강되어진다.
- 한명의 학생은 여러개의 과목을 수강한다.
- 하나의 과목은 여러 학생들에게 수강되어진다.
- 최종적으로 회원:이메일은 `n:m`이다.
- 무조건 table 생성하고 FK를 모은다.

### 6.4. ERD 그리기
