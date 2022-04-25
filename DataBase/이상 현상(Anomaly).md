# [DB] 이상 현상(Anomaly)

# 1. 이상 현상(Anomaly)

- 테이블을 설계할 때 잘못된 설계로 인하여 데이터를 삭제, 수정, 삽입할 때 논리적인 오류가 발생하는 현상
- 삽입 이상, 삭제 이상, 갱신 이상

## 1-1. 삽입 이상(Insertion Anomaly)

- 원하는 데이터만 테이블에 삽입하고자 할 때 테이블에 필요하지 않은 데이터 때문에 원치 않는  필드의 값도 삽입해야 하는 경우
- 불필요한 정보를 함께 저장하지 않고서는 어떤 정보를 저장하는 것이 불가능한 경우
    
    ![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A7%E1%86%AB%E1%84%89%E1%85%A1%E1%86%BC(Anomaly)%20c3931ee87a4c4ce88f2bfcf54859932c/Untitled.png)
    

## 1-2. 삭제 이상(Deletion Anomaly)

- 필요한 정보를 함께 삭제하지 않고서는 어떤 정보를 삭제하는 것이 불가능한 경우
- 내가 원하는 값만 테이블에서 삭제하고자 할 때 하나의 튜플이 다른 속성값도 가지고 있어 같이 지워지는 경우
    
    ![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A7%E1%86%AB%E1%84%89%E1%85%A1%E1%86%BC(Anomaly)%20c3931ee87a4c4ce88f2bfcf54859932c/Untitled%201.png)
    
    - 운영체제 성적 82라는 정보만 삭제하려고 함
    - 테이블이 더 많은 수의 필드로 구성되어 있음
    - **지우고 싶지 않은 필드들의 정보도 같이 지워야한다**.

## 1-3. 갱신 이상(Update Anomaly)

- 어떤 데이터를 수정했을 때 해당 데이터와 연관된 튜플의 모든 데이터를 찾아서 수정해야함
- 일부만 바꾸게 되어 데이터가 불일치하게되는 경우
    
    ![Untitled](%5BDB%5D%20%E1%84%8B%E1%85%B5%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A7%E1%86%AB%E1%84%89%E1%85%A1%E1%86%BC(Anomaly)%20c3931ee87a4c4ce88f2bfcf54859932c/Untitled%202.png)
    

# 2. 예시

- 테이블 구조
    - {Student ID, Course ID, Department, Course ID, Grade}
- 삽입 이상
    - 기본키가 {Student ID, Course ID} 인 경우
    - Course를 수강하지 않은 학생은 Course ID가 없는 현상이 발생
    - 결국 Course ID를 Null로 할 수밖에 없는데, 기본키는 Null이 될 수 없으므로, Table에 추가될 수 없음
- 삭제 이상
    - 어떤 학생의 전공 (Department) 이 "컴퓨터에서 음악"으로 바뀌는 경우
    - 모든 Department를 "음악"으로 바꾸어야 함
    - 일부를 깜빡하고 바꾸지 못하는 경우
    - 제대로 파악 못함
- 갱신 이상
    - 어떤 학생이 수강을 철회하는 경우
    - {Student ID, Department, Course ID, Grade}의 정보 중 Student ID, Department 와 같은 학생에 대한 정보도 함께 삭제됨

### [출처]

[https://1000hg.tistory.com/22](https://1000hg.tistory.com/22)

[https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Database/[DB] Anomaly.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Anomaly.md)