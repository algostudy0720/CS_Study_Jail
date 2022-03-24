# [AL] Tree

# 1. Tree

- Node와 Edge로 이루어진 자료구조
- 나무의 뿌리 같은 가계도 형태

![Untitled](%5BAL%5D%20Tree%20c1f4e/Untitled.png)

## 1-1. 용어 정리

- Node : Tree에서 데이터를 저장하는 기본 요소
- Edge : Node와 연결된 Node의 정보(간선)
- Root Node : 최상단에 위치하는 노드
- Level : 최상위노드를 Level 0으로 하였을 때 하위 edge로 연결된 노드의 깊이
- Parent Node : 어떤 노드의 이전 레벨에 연결된 노드
- Child Node : 어떤 노드의 상위 레벨에 연결된 노드
- Leaf Node : Child Node가 존재하지 않는 노드
- Sibling(Brother Node) : 동일한 Parent Node를 가진 같은 Level의 노드
- Depth : 트리에서 노드가 가질 수 있는 최대 Level

## 1-2. 트리의 특징

- 사이클이 존재할 수 없음 → 사이클이 존재한다? ⇒ 그래프
- 모든 노드는 자료형으로 표현이 가능
- 루트에서 임의의 한 노드로 이동하는 경로는 유일
- 노드의 갯수가 N개면 간선은 N-1개 존재

## 1-3. 트리의 순회 방식

![Untitled](%5BAL%5D%20Tree%20c1f4e/Untitled%201.png)

1. 전위 순회(Pre Order)
    - Root Node를 시작으로 왼쪽 자식 → 오른쪽 자식 노드 순으로 순회
    - 1 → 2 → 4 → 8 → 9 → 5  → 10 → 11 → 3 → 6 → 13 → 7 → 14
    
2. 중위 순회(In Order)
    - 가장 왼쪽 자식 노드를 시작으로 parent Node → 오른쪽 자식 노드 순으로 순회
    - 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 6 → 13 → 3 → 14 → 7
    
3. 후위 순회(Post Order)
    - 가장 왼쪽 자식 노드를 시작으로 오른쪽 자식 노드 → 부모 노드 순으로 순회
    - 8 → 9 → 4 → 10 → 11 → 5 → 2 → 13 → 6 → 14 → 7 → 3 → 1
    
4. 레벨 순회(Level Order)
    - Root 노드로 시작해서 왼쪽부터 Level 순으로 순회
    - 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 12 → 13 → 14