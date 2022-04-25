# [DB] 인덱스(Index)

# 1. 인덱스(Index)

- 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조
- 테이블의 컬럼을 색인화 ⇒ 목차를 만든다고 생각
- 데이터 베이스 안의 레코드를 처음부터 찾지 않고 B+ Tree로 구성된 구조에서 Index 파일 검색으로 속도를 향상시킴
    
    ![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%83%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B3(Index)%20393a3713623e40839f37f51359c4f2d6/Untitled.png)
    
    - 특정 컬럼에 인덱스를 생성하면 해당 컬럼의 데이터를 정렬하여 별도의 메모리 공간에 데이터의 물리적 주소를 함께 저장
    - 인덱스 생성 컬럼을 Where에 조건으로 거는 작업 등을 하면 생성된 인덱스를 사용하여 검색 속도 향상을 가져올 수 있음

## 1-1. 인덱스의 사용 이유

- Where절의 효율성 향상
    - 인덱스 테이블은 데이터가 정렬되어 있어 조건에 맞는 테이블을 빠르게 찾을 수 있음
- Order By절의 효율성 향상
    - 이미 정렬이 되어있는 상태이기 때문에 Sort 과정을 피할 수 있음
- MIN, MAX의 효율적인 처리
    - 데이터가 정렬되어 있으므로 레코드의 시작과 끝만 조회하면 됨

## 1-2. 인덱스의 단점

- 데이터가 항상 정렬된 상태를 유지해야 함
    - 레코드 내에 INSERT, UPDATE, DELETE를 통해 데이터가 바뀐다면 인덱스 테이블을 다시 정렬해야 함
    - 인덱스 테이블도 다시 수정해야 함
- 인덱스를 관리하기 위한 추가 저장공간이 필요함
- 인덱스를 관리하기 위한 추가 작업이 필요함

## 1-3. 인덱스의 관리

- 인덱스는 DML 작업이 발생하면 정렬 작업이 동반되므로 데이터의 삭제 대신 인덱스를 사용하지 않는다는 개념으로 관리한다.
- INSERT
    - 새로운 데이터에 대한 인덱스를 추가
- DELETE
    - 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 수행
- UPDATE
    - 기존 인덱스를 사용하지 않음 처리하고 갱신된 데이터의 인덱스를 추가

# 2. 인덱스(Index)의 자료구조

## 2-1. 해시 테이블

![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%83%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B3(Index)%20393a3713623e40839f37f51359c4f2d6/Untitled%201.png)

- 빠른 데이터 검색이 필요한 경우 유용
- 값이 1bit라도 달라지면 완전히 다른 해시값을 생성하기 때문에 등호(=)연산에 특화
- 부등호 연산(<, >)이 자주 사용되는 데이터베이스 검색에는 부적합

## 2-2. B+ Tree 테이블

![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%83%E1%85%A6%E1%86%A8%E1%84%89%E1%85%B3(Index)%20393a3713623e40839f37f51359c4f2d6/Untitled%202.png)

- 리프노드만 인덱스와 데이터를 가짐
- 나머지 노드들은 인덱스만 가짐
- 리프노드들은 Linked List로 연결
- 리프 노드의 크기와 인덱스 노드의 크기가 같지 않아도 됨
- B Tree의 리프 노드들을 Linked List로 연결하여 순차 검색을 용이하게 한 B+ Tree로 구성

### [출처]

[https://mangkyu.tistory.com/96](https://mangkyu.tistory.com/96)

[https://choicode.tistory.com/27](https://choicode.tistory.com/27)

[https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Database/[DB] Index.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Index.md)