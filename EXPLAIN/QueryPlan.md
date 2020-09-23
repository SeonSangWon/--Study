2020.09.23   

# EXPLAIN PLAN
---------------------------------------------------------------------

## EXPLAIN PLAN(실행계획)이란??
 - SQL문의 액세스 경로를 확인하고 튜닝할 수 있도록 SQL문을 분석, 해석하여 실행계획을 수립한 뒤   
   PLAN_TABLE 에 저장하는 명령이다. (쉽게 말하면 SQL문이 어떻게 실행되고 동작하는지 점검하기 위한 기능)   
   
   
 - id : 쿼리 안에 있는 각 select 문에 대한 순차 식별자이다. 이순서대로 select문이 실행된다   
 - select_type : select 문의 유형을 말한다. 각 유형은 아래와 같다   
   + SIMPLE : 서브쿼리나 'union'이 없는 가장 단순한 select문   
   + PRIMARY : 가장 바깥에 있는 select 문   
   + DERIVED : from 문 안에있는 서브쿼리의 select 문   
   + UBQUERY : 가장 바깥의 select 문에 있는 서브쿼리   
   + DEPENDENT SUBQUERY : 기본적으로 SUBQUERY와 같은 유형이며, 가장 바깥의 select 문에 '의존성'을 가진 서브쿼리의 select 문   
   + UNION : union 문의 두번째 select 문   
   + DEPENDENT UNION : 바깥 쿼리에 의존성을 가진 union 문의 두번째 select 문   
 - table : 참조되는 테이블   
 - type : MySQL이 어떤식으로 테이블들을 조인하는지를 나타내는 항목, 이 타입을 분석함으로써 어떤 인덱스가 사용되고 사용되지 않았는지를 알 수 있고, 이를통해   
   어떤식으로 쿼리가 튜닝되어야하는지에 대한 insight를 제공, insight 의 유형은 아래와 같다   
   + system : 0개 또는 하나의 row를 가진 테이블   
   + const : 테이블에 조건을 만족하는 레코드가 하나일 때, 상수 취급   
   + eq_ref : primary key 나 unique not null column 으로 생성된 인덱스를 사용해 조인을 하는 경우이다. const 방식 다음으로 빠른 방법이다   
   + index_merge   
   + unique_subquery : 오직 하나의 결과만을 반환하는 'IN'이 포함된 서브쿼리의 경우   
   + range : 특정한 범위의 rows들을 매칭시키는데 인덱스가 사용된 경우이다. BETWEEN이나 IN, '>', '>=' 등이 사용될 때이다   
   + all : 조인시에 모든 테이블의 모든 row를 스캔하는경우이다. 물론 성능이 가장 좋지 않다   
 - possible_keys : 테이블에서 row를 매핑시키기 위해 사용 가능한 (사용하지 않더라도) 키를 보여준다   
 - key : 실제적으로 쿼리 실행에 사용된 key의 목록이다. 이 항목에는 possible_keys 목록에 나타지 않은 인덱스도 포함 될 수 있다   
 - ref : key column에 지정된 인덱스와 비교되는 column 또는 constants를 보여준다   
 - rows : 결과 산출에 있어서 접근되는 record의 숫자이다. 조인문이나 서브쿼리 최적화에 있어서 중요한 항목이다   
 - Extra : 실행계획에 있어서 부가적인 정보를 보여준다
   + distinct : 조건을 만족하는 레코드를 찾았을 때 같은 조건을 만족하는 또 다른 레코드가 있는지 검사하지 않음   
   + not exist : left join 조건을 만족하는 하나의 레코드를 찾았을 때 다른 레코드의 조합은 더 이상 검사하지 않는다   
   + range checked for each record : 최적의 인덱스가 없는 차선의 인덱스를 사용한다는 의미   
   + using filesort : mysql이 정렬을 빠르게 하기 위해 부가적인 일을 한다   
   + using index : select 할때 인덱스 파일만 사용   
   + using temporary : 임시 테이블을 사용한다. order by 나 group by 할때 주로 사용   
   + using where : 조건을 사용한다는 의미   



[source](https://denodo1.tistory.com/306)   
