# MariaDB

- MySql 은 유료 입니다.
- MySql 이 유료로 바뀌기 전에 git 을 포크해서 만들어진 것이 MariaDB
- 문법이 99.9% 동일하다고 보시면 됩니다.
- https://mariadb.org/download/?os=windows&cpu=x86_64&pkg=msi&mirror=blendbyte&t=mariadb&p=mariadb&r=11.7.2

## 설치 시 주의 사항

- port 충돌 : `3308` 번으로 변경(3306 - MySql 용 포트 충돌)
- 비번 : `1234`
- 설치중 한글 사용 체크
  - `Use UTF8 as default character set and collation`
  - 문자를 입력할때 한글 및 다양한 언어들이 정상적으로 입력되도록 하는 옵션

## Path 설정

- 하단의 윈도우 검색창에서 `환경 변수 편집` 검색
- `환경변수 버튼` 클릭 후 > 하단의 시스템 변수 > `Path` 항목 더블클릭 수정 진입
- `C:\Program Files\MariaDB 11.6\bin` 추가
- 저장 완료

## SQL 구문으로 스키마 즉 데이터베이스 생성하기

```sql
-- 데이터베이스 목록보기
show databases;

-- 데이터베이스 즉 스키마 만들기
create database board;

-- 데이터베이스 목록보기
show databases;
```

## SQL 구문으로 스키마(데이터베이스) 안에 Table 생성 및 컬럼명, 컬럼 속성 셋팅하기

```sql
-- 스키마(데이터베이스)에 표를 생성한다.
-- 어느 스키마를 쓸지 결정을 해주어야 한다.
use board;
```

- author 테이블 생성하기

```sql
-- create table 테이블명
create table author(
   id int primary key, -- pk 로 항목의 제약 조건을 지정함.
   name varchar(100),
   email varchar(30),
   password varchar(20)
);
```

- 실행된 sql 구문보기

```sql
-- 실행이 된 쿼리 다시 보기
show create table author;
```

- 실행이 이루어진 구문

```sql
CREATE TABLE `author` (
   `id` int(11) NOT NULL,
   `name` varchar(100) DEFAULT NULL,
   `email` varchar(30) DEFAULT NULL,
   `password` varchar(20) DEFAULT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- posts 테이블 만들기

```sql
-- board 스키마(데이터베이스) 에 posts 테이블 생성하기
create table posts(
   id int,
    title varchar(255),
    content varchar(3000),
    author_id int not null, -- FK
    primary key(id),
    foreign key (author_id) references author(id)
);

-- 실행이 된 쿼리 다시 보기
show create table posts;
```

- 실행 결과

```sql
CREATE TABLE `posts` (
   `id` int(11) NOT NULL,
   `title` varchar(255) DEFAULT NULL,
   `content` varchar(3000) DEFAULT NULL,
   `author_id` int(11) NOT NULL,
   PRIMARY KEY (`id`),
   KEY `author_id` (`author_id`),
   CONSTRAINT `posts_ibfk_1` FOREIGN KEY (`author_id`) REFERENCES `author` (`id`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- 테이블 변경하기

```sql
-- 테이블명 변경하기
use board; -- board 스키마 사용하겠다는 쿼리
```

## 테이블 및 속성 변경 문법(ALTER)

- 테이블명 변경하기

```sql
use 스키마명

use board; -- board 스키마 사용하겠다는 쿼리

alter table 테이블명 rename 새테이블명

-- 테이블명 변경
alter table posts rename post;
-- 테이블 목록보기
show tables;

-- 테이블명 변경
alter table post rename posts;

-- 테이블 목록보기
show tables;

```

- 테이블에 컬럼 추가하기

```sql
alter table 테이블명 add colum 컬럼명 데이터타입

-- author 테이블에 age int 컬럼 추가하기
alter table author add column age int;

-- 상세정보 보기
describe author;
```

- 테이블에 컬럼 삭제하기

```sql
alter 테이블명 drop colum 칼럼명

-- author 테이블에 age 칼럼 삭제하기
alter table author drop column age;

-- 상세정보 보기
describe author;
```

- 칼럼명 변경하기

```sql
alter table 테이블명 change colum 칼럼명 새칼럼명 데이터타입;

-- posts 테이블에 content 를 contents 로 변경
alter table posts change column content contents varchar(3000);

-- 상세정보 보기
describe posts;
```

- 특정 컬럼에 속성을 변경하기

```sql
alter table 테이블명 modify column 컬럼명 데이터타입 제약 조건;

-- autor 테이블에 email 컬럼 변경하기
alter table author modify column email varchar(30) not null;

-- 상세정보 보기
describe author;

-- posts 테이블에 title 칼럼의 속성을 변경
alter table posts modify column title varchar(255) not null;

-- 상세정보 보기
describe posts;
```

## 데이터 추가(INSERT)

- 테이블에 새로운 데이터(레코드) 추가

```sql
insert into 테이블명 (컬럼명, 컬럼명, ... ) values (값, 값, ...)

-- 상세정보 보기
describe author;

-- 레코드 추가
insert into author (id, name, email, password ) values (1, '홍길동', 'hong@naver.com', '1234' );

-- 레코드 내용 전체 출력
select * from author;


-- 상세정보 보기
describe posts;

-- author 테이블에 id 가 존재하는 레코드를 posts 에 추가
insert into posts (id, title, contents, author_id) values (1, "react", "react...", 1);

-- 전체 레코드 출력
select * from posts;

-- author 테이블에 id 가 존재하지 않는 경우 레코드를 posts 에 추가
insert into posts (id, title, contents, author_id) values (2, "java", "java...", 2); -- 거부됨

-- 전체 레코드 출력 (변화가 없다.)
select * from posts;

```

## 데이터 수정(UPDATE)

```sql
update 테이블명 set 칼럼명 = 값;
```
