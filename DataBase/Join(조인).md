# [DB] 조인(Join)

# 1. Join

- 둘 이상의 테이블을 연결해서 데이터를 검색하는 방법
- 각 테이블을 연결하려면 둘 이상의 테이블이 적어도 하나의 컬럼을 공유하고 있어야 함

# 2. Join의 종류

1. Inner Join
    - 두 테이블이 Join할 때 두 테이블에 모두 지정한 열의 데이터가 존재해야 함
2. Outer Join
    - 두 테이블이 Join할 때 1개의 테이블에만 데이터가 존재하여도 Join이 가능
    1. Left Outer Join
    2. Right Outer Join
    3. Full Outer Join
3. Cross Join
    - 각 테이블의 모든 행을 Join
4. Self Join
    - 자신의 테이블과 자신의 테이블을 Join

## 2-1. Inner Join

![Untitled](%5BDB%5D%20%E1%84%8C%E1%85%A9%E1%84%8B%E1%85%B5%E1%86%AB%20ddedc/Untitled.png)

- 교집합
- 기준 테이블과 Join 테이블의 중복된 값

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## 2-2. Outer Join

![Untitled](%5BDB%5D%20%E1%84%8C%E1%85%A9%E1%84%8B%E1%85%B5%E1%86%AB%20ddedc/Untitled%201.png)

### 2-2-1. Left Outer Join

- 기준 테이블과 Join 테이블의 중복된 값
- 왼쪽 테이블을 기준으로 Join

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### 2-2-2. Right Outer Join

- Left Outer Join과 반대로 오른쪽 테이블을 기준으로 Join

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### 2-2-3. Full Outer Join

- 합집합
- A와 B 테이블의 모든 데이터를 검색

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

## 2-3. Cross Join

![Untitled](%5BDB%5D%20%E1%84%8C%E1%85%A9%E1%84%8B%E1%85%B5%E1%86%AB%20ddedc/Untitled%202.png)

- 모든 경우의 수를 전부 표현
- A가 3개, B가 3개면 총 3*3 = 9개의 데이터가 검색

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```

## 2-4. Self Join

![Untitled](%5BDB%5D%20%E1%84%8C%E1%85%A9%E1%84%8B%E1%85%B5%E1%86%AB%20ddedc/Untitled%203.png)

![Untitled](%5BDB%5D%20%E1%84%8C%E1%85%A9%E1%84%8B%E1%85%B5%E1%86%AB%20ddedc/Untitled%204.png)

- 자기 자신과 자기 자신을 join
- 하나의 테이블을 복사해서 Join한다고 생각
- 자신이 가진 컬럼을 변형시켜 활용할 떄 사용

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```

### [출처]

[https://hongong.hanbit.co.kr/sql-기본-문법-joininner-outer-cross-self-join/](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)

[https://coding-factory.tistory.com/87](https://coding-factory.tistory.com/87)