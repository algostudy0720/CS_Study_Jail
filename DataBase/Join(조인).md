# 1. Join

- 둘 이상의 테이블을 연결해서 데이터를 검색하는 방법
- 각 테이블을 연결하려면 둘 이상의 테이블이 적어도 하나의 컬럼을 공유하고 있어야 함

<br/>

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

<br/>

## 2-1. Inner Join

![Untitled](https://user-images.githubusercontent.com/45481007/163798061-f960e100-a7bc-4502-a397-19bed970d82a.png)

- 교집합
- 기준 테이블과 Join 테이블의 중복된 값

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```
<br/>

## 2-2. Outer Join

![Untitled 1](https://user-images.githubusercontent.com/45481007/163798068-6566d0f5-c212-4cd1-a7f1-12aac7027602.png)

### 2-2-1. Left Outer Join

- 기준 테이블과 Join 테이블의 중복된 값
- 왼쪽 테이블을 기준으로 Join

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```
<br/>

### 2-2-2. Right Outer Join

- Left Outer Join과 반대로 오른쪽 테이블을 기준으로 Join

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```
<br/>

### 2-2-3. Full Outer Join

- 합집합
- A와 B 테이블의 모든 데이터를 검색

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```
<br/>

## 2-3. Cross Join

![Untitled 2](https://user-images.githubusercontent.com/45481007/163798072-36c531aa-59f2-481b-a565-331a3107c625.png)

- 모든 경우의 수를 전부 표현
- A가 3개, B가 3개면 총 3*3 = 9개의 데이터가 검색

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
```
<br/>

## 2-4. Self Join

![Untitled 3](https://user-images.githubusercontent.com/45481007/163798077-b6bba8c9-bf63-4d7e-9ef0-f285205407fa.png)
![Untitled 4](https://user-images.githubusercontent.com/45481007/163798086-47e3f372-5c92-42ea-ba52-9a8498e05506.png)

- 자기 자신과 자기 자신을 join
- 하나의 테이블을 복사해서 Join한다고 생각
- 자신이 가진 컬럼을 변형시켜 활용할 떄 사용

```
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```
<br/>

### [출처]

[https://hongong.hanbit.co.kr/sql-기본-문법-joininner-outer-cross-self-join/](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)

[https://coding-factory.tistory.com/87](https://coding-factory.tistory.com/87)
