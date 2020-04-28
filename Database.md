2020.01.20

## WITH 구문 사용방법
 - WITH alias명 AS ( SUB Query )   
   SELECT column명 FROM alias명;   
   WITH aa AS   
   ( SELECT * FROM DUAL )   
   SELECT * FROM aa;
   
## 2개 이상 WITH 구문 사용방법
 - WITH alias명 AS ( SUB Query )    
   alias명2 AS ( SUB Query2 )   
   SELECT column명 FROM alias명 WHERE 조인조건;
   
---------------------------------------------------------------------
## DELIMITER(델리미터)
 - '구문 문자'로써 C 또는 JAVA 의 ';'(세미클론)과 같은 의미를 갖는다.
 - 즉, 문법읠 끝을 나타내는 역할
 - 사용방법
   + SELECT * FROM EMP$$   
   + DELIMITER $$   
     BEGIN   
        DECLARE i INT;   
        SET i = 0;   
        WHILE i < 10000 DO   
           INSERT INTO EMP(EMPNO) VALUES(i);   
           SET i = i + 1;   
        END WHILE;   
     END $$   
     DELMITER
    + DELIMITER 를 설정하지 않으면 문장을 구분하기 어렵기 때문에 세미클론이 아닌 $$ 로 설정한 것
    + 프로시저 생성 시, 필수적인 요소는 X

---------------------------------------------------------------------
2020.01.21

## INNER JOIN, LEFT/RIGHT OUTER JOIN
 - LEFT/RIGHT OUTER JOIN   
   SELECT   
          COUNT		AS 고객수   
    FROM	 TABLE_NAME1   
    LEFT		OUTER JOIN TABLE_NAME2   
          ON TABLE_NAME1.A = TABLE_NAME2.A   
   WHERE		TABLE_NAME1.A BETWEEN '20200101' AND '20200331';
 - INNER JOIN
   SELECT   
          COUNT		AS 고객수   
    FROM	 TABLE_NAME1   
   INNER  JOIN TABLE_NAME2   
          ON TABLE_NAME1.A = TABLE_NAME2.A   
   WHERE		TABLE_NAME1.A BETWEEN '20200101' AND '20200331';

---------------------------------------------------------------------
2020.01.28

## Sub Query
 - 다중형 서브쿼리
   + IN : 서브쿼리의 결과에 존재하는 임의의 값과 동일한 조건을 의미한다
   + ALL : 서브쿼리의 결과에 존재하는 모든 값을 만족하는 조건을 의미한다
   + ANY : 서브쿼리의 결과에 존재하는 어느 하나의 값이라도 만족하는 조건을 의미한다
   + EXISTS : 서브쿼리의 결과를 만족하는 값이 존재하는지 여부를 확인하는 조건을 의미한다
 - FROM 절에 사용하는 서브쿼리
   + 기본적으로 FROM 절에는 테이블 명이 오도록 되어있지만 서브쿼리가 FROM 절에 사용되면 동적으로 생성된 테이블인 것처럼   
     사용할 수 있다
   + Inline View 는 SQL 문이 실행될 때만 임시적으로 생성되는 동적인 뷰이므로 데이터베이스에 저장되지 않는다
   + 동적으로 JOIN 방식을 사용하는 것과 같다
   
---------------------------------------------------------------------
2020.01.29

## Database Migration
 - Database Migration 이란 테이블 스키마 버전 관리이다
 - 열 이름을 변경하거나 하는 이력을 마이그레이션 코드로 남겨두고 필요할 때마다 마이그레이션을   
   실행했다가 롤백하는 작업을 자유롭게 가능하다
 - 테이블을 지우기 전에 해야할 것
   + 외래키 설정 Off (다른 테이블과 관계가 형성되면 오류가 생길 수 있다)   
     mysql> set foreign_key_checks = 0 (0 : Off / 1 : On)
     
## Migration
 - 한 운영환경으로부터, 대개의 경우 조금 더 낫다고 여겨지는 다른 운영환경으로 옮겨가는 과정을 의미한다
 - Windows 운영체제에서 사용하던 프로그램을 Linux 운영체제로 그대로 옮겨 사용하는 것을 의미한다
 - 단순히 C -> Java 로 언어를 변경하는 것과는 의미가 다르다
