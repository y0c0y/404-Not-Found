
너비 우선 검색(Breadth - First Search)


[![](https://blog.kakaocdn.net/dn/buw2l2/btsyPAs89OK/dFQ7lqLsRUfoQZazwdNjlk/img.gif)](https://sunho-doing.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%83%90%EC%83%89-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-DFS-BFS)
출처: 선호:하다

그래프와 트리의 가까운 노드 부터 탐색하는 알고리즘

- 큐(Queue) 자료구조를 이용
- 왼쪽 -> 오른쪽으로 검색
- 한 레벨에서 검색을 마치면 다음 레벨로 내려가는 방법

**장점**

- 출발 노드에서 목표 노드까지의 최단 길이 경로를 보장할 수 있음.

**단점**

- 경로가 매우 길 경우에는 많은 메모리 공간은 필요함.

**구현 - O(n)**

```Python
from collections import deque

def bfs(graph, start, visited): #BFS 메소드 정의
  queue = deque([start])
  visited[start] = True

  # 큐가 빌 때까지 반복
  while queue:
    v = queue.popleft()
    print(v, end = '')

    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True

graph = [] # 그래프를 표현하는 인접 리스트(2차원 리스트)
visited = [] # 각 노드가 방문된 정보를 표현하는 1차원 리스트

bfs(graph, 1, visited) # bfs 함수 호출
```