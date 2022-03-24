# [AL]Binary Search Tree(이진 탐색 트리)

# 1. 이진 탐색 트리

- 이진탐색 + 연결리스트의 형태
- 이진탐색
    - 탐색에 소요되는 시간 복잡도O(logN)
    - 삽입, 삭제가 어려움
- 연결리스트
    - 삽입, 삭제의 시간복잡도 O(1)
    - 탐색하는 시간 복잡도 O(N)

⇒ 탐색 시간 小, 삽입. 삭제 가능

![Untitled](%5BAL%5DBinary%203acf8/Untitled.png)

## 1-1. BST의 특징

- 각 노드마다 자식 노드가 2개 이하
- 각 노드의 왼쪽 자식은 부모 노드보다 작고, 오른쪽 자식은 부모보다 큼
- 중복된 노드가 없어야 함
    - 검색을 목적으로 하는 자료구조인데 중복이 많다면 굳이 트리를 사용하여 검색 속도를 느리게 할 필요가 없음
    - 같은 값을 가지는 노드에 count 변수를 통해 중복을 관리하게 하는 것이 일반적
- 각 서브 트리들도 BST를 이룸
- 중회 순회(왼쪽 → 루트 → 오른쪽)를 통해 정렬된 순서로 탐색 가능

## 1-2. BST 시간 복잡도

1. 균등 트리(트리가 좌우 균형있게 배분된 형태)
    - 노드 개수가 N일 때 O(logN)
2. 편향 트리(트리의 노드들이 한 쪽으로 몰린 형태)
    
    ![Untitled](%5BAL%5DBinary%203acf8/Untitled%201.png)
    
    - 노드 개수가 N일 때 O(N)

※ 삽입, 검색, 삭제의 시간복잡도는 트리의 Depth에 비례

## 1-3. BST에서의 노드 삭제

1. 자식이 없는 Leaf 노드
    - 그냥 삭제
2. 자식이 1개인 노드
    - 노드 삭제
    - 지워진 노드 위치에 자식 노드를 배치
3. 자식이 2개인 노드
    - 노드 삭제
    - 오른쪽 자식 노드 중 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값
    - 둘 중에 하나를 골라 삭제한 노드 위치에 배치

※ 편향 트리(한 쪽으로만 쭉 뻗는 형태)라면 시간복잡도가 O(N)이므로 굳이 트리 구조를 사용할 이유가 없음

→ 균형 트리로 바꾸어줘야함

⇒ AVL Tree, B Tree 등

## 1-4. 면접 질문

### Q. BST와 Binary Tree에 대해 설명하세요.

ANS)

- 이진 트리
    - 모든 노드들이 최대 2개의 자식 노드를 가지는 형태의 트리
- 이진 탐색 트리
    - 탐색을 위해 특정 규칙 하에 구성된 이진 트리
    - 한 노드의 모든 왼쪽 자식 노드는 부모 노드보다 작아야한다.
    - 한 노드의 모든 오른쪽 자식 노드는 부모 노드보다 커야 한다.

### [출처]

[https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Data Structure/Binary Search Tree.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Binary%20Search%20Tree.md)

[https://velog.io/@humblechoi/자료구조-트리와-힙](https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%A6%AC%EC%99%80-%ED%9E%99)

### [참조 코드]

[https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Data Structure/code/binarySearchTree.java](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/code/binarySearchTree.java)