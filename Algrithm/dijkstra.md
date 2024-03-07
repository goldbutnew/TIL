# 이금현

### 최단 경로 문제란?

- 각 간선의 가중치 합이 최소가 되는 두 정점(또는 노드) 사이의 경로를 찾는 문제
    - 정점(vertex): 교차로
    - 간선(edge): 길
    - 가중치(weight): 거리나 시간 같은 이동 비용
- 대표 알고리즘: 다익스트라

### 다익스트라 알고리즘

- 가중치가 음수인 경우는 처리할 수 없음
- 최장 거리를 구하는 데에는 다익스트라 알고리즘 사용 불가

### 우선순위 큐를 이용한 다익스트라 알고리즘

- 파이썬에서 우선 순위 큐를 최소 힙으로 구현한 모듈 `heapq` 사용

```python
import heapq

def networkDelayTime(times, N, K):
    graph = {}

    # 그래프 인접 리스트 구성
    for u, v, w in times:
        if u not in graph:
            graph[u] = []
        graph[u].append((v, w))

    # 큐 변수: [(소요시간, 정점)]
    Q = [(0, K)]
    dist = {}

    # 우선 순위 큐 최솟값 기준으로 정점까지 최단 경로 삽입
    while Q:
        time, node = heapq.heappop(Q)
        if node not in dist:
            dist[node] = time
            if node in graph:
                for v, w in graph[node]:
                    alt = time + w
                    heapq.heappush(Q, (alt, v))

    # 모든 노드의 최단 경로 존재 여부 판별
    if len(dist) == N:
        return max(dist.values())
    return -1

```