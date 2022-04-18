# [DB] SQL Injection

# 1. SQL Injection

- 악의적인 사용자가 보안상의 취약점을 이용하여 임의의 SQL문을 주입하고 실행하여 서버의 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

# 2. SQL Injection 공격 방법

1. 인증 우회
    - SQL Injection 공격의 대표적인 경우
    - 로그인 Form을 대상으로 공격 수행
    - 정상적인 계정 정보 없이도 로그인하여 인증을 획득할 수 있다.

예시)

```sql
SELECT * FROM USER WHERE ID = "abc" AND PASSWORD = "1234";
=>
1234; DELETE * USER FROM ID = "1";
```

```sql
[ 외부 입력값 ]
UserID: test
Password: 1234' or '1'='1

[ 실행되는 쿼리문 ]
Select * From Users Where UserID = 'test' And Password='1234' or '1'='1'
```

1. 데이터 노출
    - 시스템에서 발생하는 에러메시지를 이용하는 공격 방식
    - 의도적으로 SQL 구문 에러를 유발하여 서버에서 반환되는 오류 정보를 기반으로 하여 DB 정보 유출

예시)

```sql
[ 외부 입력값 ]
UserID: test' UNION SELECT 1 --
Password: 아무거나

[ 실행되는 쿼리문 ]
Select * From Users Where UserID = 'test' UNION SELECT 1 -- And Password='아무거나'

[오류]
"UNION, INTERSECT 또는 EXCEPT 연산자를 사용하여 결합된 모든 쿼리의 대상 목록에는 동일한 개수의 식이 있어야 합니다." (SQL Server 기준)

```

- 컬럼 수가 몇 개인지 정보를 얻을 수 있음

1. 시스템 명령어 실행
    
    ```sql
    [ 외부 입력값 ]
    UserID: admin' ; EXEC master.dbo.xp_cmdshell 'cmd.exe dir c:'--
    Password: 아무거나
    
    [ 생성된 쿼리문 ]
    Select * From Users Where UserID = 'admin' ; EXEC master.dbo.xp_cmdshell 'cmd.exe dir c:'-- And Password='아무거나'
    
    ```
    
    - 다음과 같이 Shell 명령어를 이용하여 시스템 명령을 내릴 수 있다.
    

# 3. SQL Injection 방어 방법

1. Input 값을 받을 때, 특수문자 여부 검사하기
    - 로그인 전, 검증 로직을 추가하여 미리 설정한 특수문자들이 들어왔을 때 요청을 무시함
2. SQL 서버 오류 발생 시, 해당하는 에러 메시지 감추기
    - View를 활용하여 원본 데이터베이스 테이블에는 접근 권한을 높임
    - 일반 사용자는 View로만 접근하여 에러를 볼 수 없도록 함
3. Preparestatement 사용하기
    - Preparedstatement를 사용하면 특수 문자를 자동으로 걸러준다.
    - 전달인자 값을 ?로 받음
    - 이를 통해 서버측에서 필터링을 거침

※ View

- 가상 테이블
- 전체 데이터 중에서 일부만 접근 가능
- 사용자마다 특정 객체만 조회할 수 있도록 기능 제공(데이터 접근 제어)

### [출처]

[https://m.mkexdev.net/427](https://m.mkexdev.net/427)