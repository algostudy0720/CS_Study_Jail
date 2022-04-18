# 1. 최소 공통 조상(LCA, Lowest Common Ancester)

- 트리 구조에서 임의의 두 정점이 가지는 가장 가까운 조상 정점

![Untitled](https://user-images.githubusercontent.com/45481007/163776814-9d1202a3-9753-408d-b3c8-d8e53ffc997b.png)

- 위의 트리에서 두 정점 13, 15의 공통 조상은 5가 된다.

<br/>

## 1-1. 구현 개념

- 해당 정점들의 depth와 parent를 따로 저장한다.
- 두 배열 정보를 활용하여 두 정점이 주어졌을 때 depth를 조절하며 공통 조상을 찾는다.
<br/>

## 1-2. 구현 코드

```
// depth -> 정점
0 → 1(root 정점)
1 → 2, 3
2 → 4, 5, 6, 7
```

```
// 1 ~ 7번 정점 (root는 부모가 없기 때문에 0)
int parent[] = {0, 1, 1, 2, 2, 3, 3}
```

```
// 두 정점의 depth 확인하기
while(true){
	if(depth가 일치)
		if(두 정점의 parent 일치?) LCA 찾음(종료)
      else 두 정점을 자신의 parent 정점 값으로 변경
   else // depth 불일치
      더 depth가 깊은 정점을 해당 정점의 parent 정점으로 변경(depth가 감소됨)
}
```
<br/>

## 1-3. 예시

![Untitled 1](https://user-images.githubusercontent.com/45481007/163776818-0b7d2428-b308-4b23-b81c-ec33cd4fb90d.png)

```jsx
void LCA(int a, int b){
  int[] depth = {0, 1, 1, 2, 2, 2, 2}; // depth[i]는 i번 노드의 depth
  int[] parent = {0, 1, 1, 2, 2, 3, 3}; // parent[i]는 i번 노드의 부모 노드 번호

  while(True){
    if(depth[a]==depth[b]){
      if(parent[a]==parent[b]){
        return parent[a];
      }
      else{
        a = parent[a];
        b = parent[b];
      }
    }
    else if(depth[a] > depth[b]){
      a = parent[a];
    }
    else {
      b = parent[b];
    }
  }
}
```
<br/>

### [출처]

[https://nooblette.tistory.com/295](https://nooblette.tistory.com/295)
