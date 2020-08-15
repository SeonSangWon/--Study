# Database
> Database Study   

------------------------------
## 데이터베이스(Database)란 ?

데이터베이스(DB: database)는 통합하여 관리되는 데이터의 집합체를 의미   

이는 중복된 데이터를 없애고, 자료를 구조화하여, 효율적인 처리를 할 수 있도록 관리한다.   
따라서, 여러 업무에 여러 사용자가 데이터 베이스를 사용할 수 있다.   

이러한 데이터베이스는 응용 프로그램과는 다른 별도의 미들웨어에 의해 관리된다.   
데이터베이스를 관리하는 이러한 미들웨어를 데이터베이스 관리 시스템(DBMS: Database Management System)이라고 한다.   

------------------------------
## 데이터베이스의 특징

데이터베이스는 다음과 같은 특징을 가진다.

>    > 1. 사용자의 질의에 대하여 즉각적인 처리와 응답이 이루어진다.
>    > 2. 생성, 수정, 삭제를 통하여 항상 최신의 데이터를 유지한다.
>    > 3. 사용자들이 원하는 데이터를 동시에 공유할 수 있다.
>    > 4. 사용자가 원하는 데이터를 주소가 아닌 내용에 따라 참조 할 수 있다.
>    > 5. 응용프로그램과 데이터베이스는 독립되어 있으므로, 데이터의 논리적 구조와 응용프로그램은 별개로 동작된다.

------------------------------
## SQL(Structured Query Language)

SQL(Structured Query Language)은 데이터베이스에서 데이터를 정의, 조작, 제어하기 위해 사용하는 언어이다.   

>    > 1. DDL(Data Definition Language)
>    > 2. DML(Data Manipulation Language)
>    > 3. DCL(Data Control Language)

<table>
    <tr>
        <td width="100" align="center">속성</td><td width="120" align="center">설명</td><td width="50" align="center">주요 명령어</td>
    </tr>
    <tr>
        <td align="center">DDL</td>
        <td>데이터베이스나 테이블 등을 생성, 삭제하거나 그 구조를 변경하기 위한 명령어</td>
        <td>CREATE, ALTER, DROP</td>
    </tr>
    <tr>
        <td align="center">DML</td>
        <td>데이터베이스에 저장된 데이터를 처리하거나 조회, 검색하기 위한 명령어</td>
        <td>INSERT, UPDATE, DELETE,<br/> SELECT 등</td>
    </tr>
    <tr>
        <td align="center">DCL</td>
        <td>데이터베이스에 저장된 데이터를 관리하기 위하여 데이터의 보안성 및 무결성 등을<br/> 제어하기 위한 명령어</td>
        <td>GRANT, REVOKE 등</td>
    </tr>
</table>
</div>

[source](http://tcpschool.com/mysql/DB)