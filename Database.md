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
