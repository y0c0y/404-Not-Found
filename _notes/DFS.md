### 깊이 우선 검색(Depth - First Search)

[![](https://blog.kakaocdn.net/dn/sf8pe/btsyOXPEADA/epkUQ7S78z5G8fhHnDxIRK/img.gif)](https://sunho-doing.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%83%90%EC%83%89-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-DFS-BFS)

출처 : 선호:하다

그래프와 트리의 깊은 부분을 우선적으로 탐색하는 알고리즘

- 스택(Stack) 자료구조를 이용
- 위쪽 -> 아래쪽으로 검색
- 리프에 도달해서 더 이상 검색할 곳이 없으면 일단 부모 노드로 돌아가고 그뒤 다시 자식 노드로 내려가는 방법

**장점**

- 현재 탐색하고 있는 경로상의 노드들만 기억하면 되기에 공간 복잡도가 비교적 작음.

- 목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있음.

**단점**

- 해가 속해 있지 않은 깊은 경로에 빠질 가능성이 있음.

- 얻어진 해가 최단 경로가 된다는 보장이 없음. 즉, 목표에 이르기 까징의 경로가 여러개인 경우 최적의 해가 아닐 가능성이 있음.

**구현 - O(n)**

``` Python
def dfs(graph, v, visited): # DFS 메소드 정의
  visited[v] = True
  print(v, end = '')

  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)

graph = [] # 그래프를 표현하는 인접 리스트(2차원 리스트)
visited = [] # 각 노드가 방문된 정보를 표현하는 1차원 리스트

dfs(graph, 1, visited) # dfs 함수 호출
```