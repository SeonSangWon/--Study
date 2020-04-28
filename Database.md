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

---------------------------------------------------------------------
2020.02.05

## 집합연산 [UNION / INTERSECT / MINUS]
 - UNION [UNION DISTINCT]
   + UNION DISTINCT 와 동일한 작업을 수행하므로 중복되는 레코드를 제거해준다
 - UNION ALL
   + 별도의 중복 제거 과정을 거치지 않고 결과를 보여준다
   
### MySQL 이 내부적으로 UNION 과 UNION ALL 을 처리하는 과정
 1. 최종 UNION [ALL | DISTINCT] 결과에 적합한 임시 테이블(Temporary Table)을 메모리 테이블로 생성
 2. UNION | UNION DINTINCT 의 경우, Temporary Table 의 모든 컬럼으로 Unique Hash Index 를 생성
 3. 서브 쿼리1 실행 후, Temporary Table 에 복사
 4. 서브 쿼리2 실행 후, Temporary Table 에 복사
 5. 만약 3,4번 과정에서 Temporary Table 이 특성 크기 이상으로 커질경우 Temporary Table 을   
   Disk Temporary Table로 변경 (이 때, Unique Hash Index 는 Unique B-Tree Index 로 변경)
 6. Temporary Table 을 읽어서 Client 에 결과 전송   
 7. Temporary Table 삭제
 
### UNION DINTINCT 와 UNION ALL 의 차이점
 - 2번 과정이 수행되어 중복 제거를 위해 Temporary Table 에 Index 를 생성하는가/생성하지 않는가 의 차이
 - Index 로 인해서 데이터의 건수에 따라 다르지만 1.5배 ~ 4배 가량의 성능 차이로 UNION ALL 이 빠르게 처리된다
 - 데이터량이 미세할 경우 메모리 Temporary Table 에 Hash Index 를 사용하기 때문에 속도 차이가   
   매우 미세하지만, 데이터량이 커져서 5번 과정을 거치고 Disk Temporary Table 에 B-Tree Index 를   
   사용하기 때문에 큰 성능차이가 발생한다
 - '중복의 기준'을 고려한다면, UNION 하는 컬럼들의 수가 많아지고 레코드의 사이즈가 커질 수록 두 작업   
   모두 불리하겠지만, UNION ALL 보다는 UNION 에 더 악영향이 클 것이다
   
 - UNION | UNION ALL 둘 다 좋은 SQL 작성은 아니므로 만약 사용해야 한다면, 최소 필요 컬럼만 SELECT 하는 것이 좋다.
