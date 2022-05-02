# 1. 트랜잭션(Transaction)

- 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위
- 데이터의 베이스의 상태를 변화시킨다는 것 ⇒ SQL 질의어를 사용하여 DB에 접근하는 것
    - SELECT
    - INSERT
    - DELETE
    - UPDATE
- 작업 단위
    - 사람이 전하는 기준에 따라 수행할 SQL문을 정하는 것
    
    ```
    예시) 사용자 A가 사용자 B에게 만원을 송금한다.
    
    * 이때 DB 작업
    - 1. 사용자 A의 계좌에서 만원을 차감한다 : UPDATE 문을 사용해 사용자 A의 잔고를 변경
    - 2. 사용자 B의 계좌에 만원을 추가한다 : UPDATE 문을 사용해 사용자 B의 잔고를 변경
    
    // 현재 작업 단위 : 출금 UPDATE문 + 입금 UPDATE문
    → 이를 통틀어 하나의 트랜잭션이라고 한다.
    
    // 발생 가능한 오류
    - 구매자의 계좌에서 돈이 출금된 뒤, DB가 다운된다.
    - 구매자의 계좌에서 돈이 출금되지 않았는데, 판매자에게 돈이 입금된다.
    - 출금도 입금도 되지 않는다.
    
    - 위 두 쿼리문 모두 성공적으로 완료되어야만 "하나의 작업(트랜잭션)"이 완료되는 것이다. `Commit`
    - 작업 단위에 속하는 쿼리 중 하나라도 실패하면 모든 쿼리문을 취소하고 이전 상태로 돌려놓아야한다. `Rollback`
    
    ```
    
<br/>

## 1-1. 트랜잭션의 특징

- 원자성(Atomicity)
    - 트랜잭션이 DB에 모두 반영되거나 혹은 전혀 반영되지 않아야 한다.
- 일관성(Consistency)
    - 트랜잭션의 작업 처리 결과는 항상 일관성이 있어야 한다.
- 독립성(Isolation)
    - 둘 이상의 트랜잭션이 동시에 실행되고 있을 때 어떤 트랜잭션도 다른 트랜잭션의 연산에 끼어들 수 없다.
- 지속성(Durability)
    - 트랜잭션이 완료되었으면 결과는 영구적으로 반영되어야 한다.
    
<br/>

## 1-2. 트랜잭션 용어

- Commit
    - 하나의 트랜잭션이 성공적으로 끝났고 DB가 일관성있는 상태일 때 DB에 이를 반영하기 위해 사용하는 연산
- Rollback
    - 하나의 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우
    - 트랜잭션이 정상적으로 종료되지 않았을 때 최종 Commit 지점으로 Rollback할 수 있음
    
<br/>

## 1-3. 트랜잭션 관리를 위한 DBMS의 전략

### 1-3-1. 이해를 위한 개념

1. DBMS의 구조
    - 질의 처리기(Query Processor)
    - 저장 시스템(Storage System)
    - 고정 길의의 Page 단위로 Disk에 읽고 쓴다.
    - 비휘발성 장치인 Disk에 저장
    - 일부는 Main Memory에 저장
    
![Untitled](https://user-images.githubusercontent.com/45481007/166223746-c94bee56-ed89-4287-9970-38f855aa80c6.png)

    
2. 1. Page Buffer Manager / Buffer Manager
    - DBMS의 저장 시스템에 속하는 모듈 중 하나
    - Main Memory에서 유지하는 Page를 관리하는 모듈
    - Buffer 관리 정책에 따라 REDO, UNDO가 요구되므로 Transaction 관리에 중요한 영향을 끼침
    
<br/>

### 1-3-2. DBMS 전략

1. UNDO
    - 수정된 Page들이 Buffer의 교체 알고리즘에 따라서 디스크에 출력 될 수 있음(MEMORY에서 DISK로 OUTPUT)
    - Buffer의 교체는 트랜잭션과 무관하게 발생하므로 종료되지 않은 Transaction이 변경한 page들은 원상복구 되어야 하는데 이 복구를 UNDO라고 함
    - 매우 큰 메모리 버퍼를 가지고 있어야 함
    - 2개의 정책(수정된 페이지를 디스크에 쓰는 시점에 따라)
        - Steal
            - 수정된 페이지를 언제든지 디스크에 쓸 수 있는 정책
            - 대부분의 DBMS가 채택하는 Buffer 관리 정책
            - UNDO Logging과 복구를 필요로 함
        - Not Steal
            - 수정된 페이지를 EOT(End Of Transaction)까지는 버퍼에 유지하는 정책
            - UNDO 작업이 필요하지 않지만 매우 큰 메모리 버퍼가 필요함
2. REDO
    - 이미 Commit한 Transaction의 수정을 재반영하는 복구 작업
    - Buffer 관리 정책에 영향을 받음
    - 2가지 정책(Transaction이 종료되는 시점에 해당 Transaction이 수정한 Page를 디스크에 쓸 지 말지에 따라)
        - Force
            - 수정했던 페이지를 Transaction Commit 시점에 Disk에 반영
            - Commit 되었을 때 수정된 페이지들이 Disk에 반영되므로 REDO 필요 없음
        - Not Force
            - Commit 시점에 반영하지 않는 정책
            - Transaction이 Disk 상의 DB에 반영되지 않을 수 있기 때문에 REDO 복구가 필요
            - 대부분의 DBMS 정책
    
     
    
<br/>
 

### [출처]

[https://velog.io/@syleemk/면접-대비-스프링-트랜잭션-전파](https://velog.io/@syleemk/%EB%A9%B4%EC%A0%91-%EB%8C%80%EB%B9%84-%EC%8A%A4%ED%94%84%EB%A7%81-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%A0%84%ED%8C%8C)
