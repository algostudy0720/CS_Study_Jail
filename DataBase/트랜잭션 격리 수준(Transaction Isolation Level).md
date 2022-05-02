# [DB] 트랜잭션 격리 수준(Transaction Isolation Level)

# 1. 격리 수준

- 트랜잭션에서 일관성 없는 데이터를 허용하도록 하는 수준

## 1-1. 격리 수준의 필요성

- DB는 ACID 특징에 따라 트랜잭션이 독립적인 수행을 함
    
    ⇒ Locking을 통해 트랜잭션 수행 중에 다른 트랜잭션의 관여를 막아야 함
    
- 무조건적인 Locking은 수많은 트랜잭션을 순서대로 처리하므로 성능 저하
- Locking의 범위를 줄이면 트랜잭션의 관여로 인해 잘못된 값이 처리될 가능성 상승

⇒ 효율적인 Locking 방법이 필요!

## 1-2. 격리 수준에 따른 분류

1. Read Uncommitted(Level 0)
    - SELECT 문장이 수행되는 동안 해당 데이터에 Lock이 걸리지 않는 계층
    - 트랜잭션이 처리중이거나 아직 Commit 되지 않은 데이터에 대해 다른 트랜잭션의 접근을 허용
        
        `사용자1이 A라는 데이터를 B라는 데이터로 변경하는 동안 사용자2는 아직 완료되지 않은(Uncommitted) 트랜잭션이지만 데이터B를 읽을 수 있다`
        
        ⇒ 일관성 유지 X
        
2. Read Committed(Level 1)
    - SELECT 문장이 수행되는 동안 해당 데이터에 Lock이 걸리는 계층
    - 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 됨
    - Commit이 이루어진 트랜잭션만 조회 가능
    - SQL 서버가 Default로 사용하는 Isolation Level
        
        `사용자1이 A라는 데이터를 B라는 데이터로 변경하는 동안 사용자2는 해당 데이터에 접근이 불가능함`
        
3. Repeatable Read(Level 2)
    - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Lock이 걸리는 계층
    - 트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장함
    - 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 불가능
4. Serializable(Level 3)
    - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Lock이 걸리는 계층
    - 완벽한 일관성을 제공
    - 다른 사용자는 트랜잭션 영역에 해당하는 데이터에 대한 수정 및 입력 불가능

## 1-3. 격리 수준 선택 시 고려사항

- 동시성과 데이터 무결성에 견관
- 동시성을 증가시키면 무결성에 문제
- 무결성을 증가시키면 동시성에 문제
- 레벨을 높게 조정할 수록 비용이 증가

## 1-4. 낮은 격리 수준 선택시 발생하는 현상

1. Dirty Read
    - 커밋되지 않은 수정중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상
    - 어떤 트랜잭션에서 아직 실행이 끝나지 않은 다른 트랜잭션에 의한 변경사항을 보게되는 경우
2. Non-Repeatable Read
    - 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션 값을 수정 또는 삭제하면서 두 쿼리의 결과가 상이하게 나타나는 일관성이 깨진 현상
3. Phantom Read
    - 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫번째 쿼리에서 없던 레코드가 두번째 쿼리에서 나타나는 현상
    - 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타나는 현상

### [출처]

[https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Database/Transaction Isolation Level.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md)