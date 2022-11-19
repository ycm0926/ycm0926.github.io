---

layout: single
title: "Ch9 Shortest Path 9-1"
categories: algorithm
tag: [python, coding, algorithm, 이것이 코딩 테스트다]
toc: true
author_profile: false
sidebar:
    nav: "docs"

---

# 📚 최단 경로 (Shortest Path) 알고리즘

**최단 경로 (Shortest Path)** 알고리즘 이란 <span style="background-color:#baddfe">말 그대로 가장 짧은 경로를 찾는 알고리즘이다.</span>
* 최단 경로 알고리즘 유형에는 다양한 종류가 존재한다.
  * 한 지점에서 다른 특정 지점까지의 최단 경로
  * 한 지점에서 다른 모든 지점까지의 최단 경로
  * 모든 지점에서 다른 모든 지점까지의 최단 경로
* 학부 수준으로 다익스트라 최단 경로 알고리즘, 플로이드 워셜, 벨만 포트 알고리즘 이렇게 3가지이다.
  * 이 책은 **다익스트라**와 **플로이드 워셜** 2가지를 다룸.
* 그리디 알고리즘과 다이나믹 프로그래밍 알고리즘이 최단 경로 알고리즘에 그대로 적용된다는 특징이 있다.

> 다익스트라의 정확한 외래어 표기는 '데이크스트라'라고 한다. 

## 다익스트라 최단 경로 알고리즘

![다익스트라](/assets/images/ch-09-최단경로그래프.png)

* **다익스트라 (Dijkstra)** 최단 경로 알고리즘은 그래프에서 여러개의 노드가 있을 때, 특정한 노드에서 출발하여 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘이다.
* '음의 간선'이 없을 때 정삭적으로 동작한다.
* 기본적으로 그리디 알고리즘으로 분류된다. 매번 '가장 작은 비용이 적은 노드'를 선택해서 임의의 과정을 반복
* 알고리즘 간략 설명
  * 1) 출발 노드를 설정한다.
  * 2) 최단 거리 테이블을 초기화한다.
  * 3) 방문하지 않은 노드 중에서 최단 거리가 짧은 노드를 선택한다.
  * 4) 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
  * 5) 위 과정에서 3)과 4)번을 반복한다.
* 알고리즘 구현 방법은 2가지.
  * 구현하기 쉽지만 느리게 동작하는 코드
  * **구현하기 조금 더 까다롭지만 빠르게 동작하는 코드**

## 다익스트라 알고리즘: 동작 과정
* 초기 상태 다른 노드로 가는 값으로는 999,999,999 또는 987,654,321 (약10억) 으로 설정하기도 한다.
* 파이썬에서 기본으로 1e9를 실수 자료형으로 처리 하는데 모든 간선이 정수형으로 표현되는 문제에서는 **int(1e9)**로 초기화.
* 단게를 거치며 <span style="background-color:#baddfe">한 번 처리된 노드의 최단 거리는 고정</span>되어 더 이상 바뀌지 않는다.
  * **한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 것으로 이해**
* 마지막 노드는 나머지 노드들의 최단 거리가 확정된 상태이므로 더 이상 테이블 갱신이 될 수 없어 확인할 필요가 없다.
* 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가적인 기능을 더 넣어야 한다.

![다익스트라](/assets/images/ch-09-다익스트라.png)
* 방문하지 않은 노드 중 가장 짧은 노드는 값이 0인 1번 노드로 출발

![다익스트라](/assets/images/ch-09-다익스트라2.png)
* 1번 노드와 연결된 모든 간선을 하나씩 확인

![다익스트라](/assets/images/ch-09-다익스트라3.png)
* 4번 노드를 거쳐 3, 5번 노드 비용과 1번 노드에서 3, 5번 노드의 비용 비교

![다익스트라](/assets/images/ch-09-다익스트라4.png)
* 일반적으로 같은 값일 경우 노드 번호가 더 낮은 값을 선택.


![다익스트라](/assets/images/ch-09-다익스트라5.png)


![다익스트라](/assets/images/ch-09-다익스트라6.png)


![다익스트라](/assets/images/ch-09-다익스트라7.png)
* 마지막 노드는 처리하지 않아도 전체 결과를 얻음
  * 나머지 5개 노드에 대한 최단 거리가 확정된 상태이므로 더 이상 테이블 갱신 불가

### 방법 1. 간단한 다익스트라 알고리즘
* 총 $O(V)$번에 걸쳐서 최단 거리가 가장짧은 노드를 매번 선형탐색 -> 전체 시간복잡도 $O(V^2)$
  * V는 노드의 개수를 의미
  * 처음 각 노드에 대한 최단 거리를 담는 1차원 리스트를 선언
  * <span style="background-color:#baddfe">단계마다 '방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택'하기 위해 매 단계마다 1차원 리스트의 모든 원소를 확인(앞에서 부터 순차적 탐색)</span>
* 노드의 개수가 5,000개 이하라면 일반적으로 가능
  * 개수가 10,000개 이상이면 이 코드로는 힘들다.

```python
# 간단한 다익스트라 알고리즘 소스코드

import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False]*(n+1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF]*(n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    # 시작 노드에서의 최단 거리 테이블 갱신
    for j in graph[start]:
        distance[j[0]] = j[1]
    # 시작 노드를 제외한 전체 n-1개의 노드에 대해 반복
    for i in range(n-1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른 노드를 확인
        for j in graph[now]:
            cost = distance[now]+j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost

# 다익스트라 알고리즘 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```
```python  
# 입력 예시 
# 1. 노드와 간선 수
# 2. 출발 노드
# 3. 출발노드, 도착노드, 간선 
6 11
1
1 2 2 
1 3 5
1 4 1
2 3 3
2 4 2
3 2 3
3 6 5
4 3 3
4 5 1
5 3 1
5 6 2

# 출력 예시
0
2
3
1
2
4
```

### 방법 2. 개선된 다익스트라 알고리즘
* <span style="background-color:#baddfe">단계마다 '방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택'</span>하기 위해 **힙(Heap)** 자료구조를 이용  (간단한 다익스트라 알고리즘은 순차 탐색을 이용)
* 다익스트라 알고리즘이 동작하는 **기본 원리는 동일**
  * 현재 가장 가까운 노드를 저장해 놓기 위해서 힙 자료구조를 추가적으로 이용한다는 점이 다르다. 
  * 현재의 최단 거리가 가장 짧은 노드를 선택해야 하므로 **최소 힙**을 사용한다.

#### 힙 설명
* 완전 이진 트리의 일종이다.
* 최대값과 최솟값을 빠르게 찾기 위해 고안된 자료구조
* 우선순위 큐(Priority Queue)를 구현하기 위해 사용하는 자료구조 중 하나.
* **최소 힙(Min Heap)**과 **최대 힙(Max Heap)**이 있다.
  * 최대 힙: 부모 노드의 키 값이 자식 노드의키 값보다 크거나 같은 완전 이진 트리
  * 최소 힙: 부모 노드의 키 값이 자식 노드의키 값보다 작거나 같은 완전 이진 트리
* 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용된다.
  
> (주의) 힙 정렬에서 말하는 '힙'과 메모리 할당 공간인 '힙'은 관련이 없다.

> **우선순위 큐는 왜 힙 자료구조를 사용할까?**
> * 이유는 **수행시간** 때문이다.
> * heap은 삽입 삭제 연산이 모두 logN이지만 배열, 리스트와 같은 선형 구조의 형태는 삽입 혹은 삭제 둘 중 하나의 연산이 극단적인 수행 시간을 갖는다.
> * 정렬이 되어있지 않은 배열과 리스트의 경우, 입력은 상수 수행시간을 가지며 우선순위에 부합하는 원소를 찾는 과정에서 최악의 경우 n 번의 연산 수행한다.
> * 정렬이 되어있는 배열과 리스트의 경우, 입력하는 과정에서 정렬을 시켜야한다 따라서 최악의 경우 n 번의 연산을 수행한다.
> * 자료구조와 알고리즘에서는 항상 최악의 상황을 고려해야 하는데 만약 n 개의 데이터 모두 최악의 경우에 놓인다면 **$n^2$**의 수행 시간을 갖게 된다.
> * 힙의 경우 모두 최악의 상황에 놓인다 가정해도 **$nlogn$**의 수행 시간을 갖는다.
> 
> ![힙](/assets/images/ch-09-힙시간비교.png)


**힙 라이브러리 사용 예제: 최소 힙**
```python
import heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
        # heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
        # result.append(-heqpq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```
실행결과
```python
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```
* heappush(): 특정 리스트에 어떤 데이터를 넣을때
* heappop(): 특정 리스트에서 데이터를 꺼낼 때 -> 우선순위대로 꺼내짐
* default는 오름차순으로 꺼내진다.
* 최대 힙을 이용하고 싶을 때는 부호를 바꿔서 넣은 뒤, 꺼낼 때 다시 부호를 바꿔주면 됨
* n개의 데이터를 넣고 빼기 때문에 전체 시간복잡도 $O(NlogN)$
  * 병합, 퀵 정렬과 비슷한 시간복잡도
* 힙 동작 과정
  ![힙](/assets/images/ch-09-힙.png)

  ![힙](/assets/images/ch-09-힙2.png)

#### 우선순위 큐 설명
* <span style="background-color:#baddfe">우선순위가 가장 높은 데이터를 가장 먼저 삭제</span>하는 자료구조.
* 예를 들어 여러 개의 물건 데이터를 자료구조에 넣었다가 가치가 높은 물건 데이터부터 꺼내서 확인해야 하는 경우에 우선순위 큐를 이용할 수 있다.
* Python, C++, Java를 포함한 대부분의 프로그래밍 언어에서 **표준 라이브러리 형태로 지원**한다.
* 파이썬은 PriorityQueue 라는 라이브러리를 제공하여 코드는 간략해 지지만 속도가 매우 느리다.

|자료구조|추출되는 데이터|
|---|---|
|스택(Stack)|가장 나중에 삽입된 데이터|
|큐(Queue)|가장 먼저 삽입된 데이터|
|우선순위 큐(Priority)|가장 우선순위가 높은 데이터|

### 다익스트라 알고리즘: 우선순위 큐 동작 과정
![우선순위큐](/assets/images/ch-09-우선순위큐.png)

![우선순위큐](/assets/images/ch-09-우선순위큐2.png)

![우선순위큐](/assets/images/ch-09-우선순위큐3.png)

![우선순위큐](/assets/images/ch-09-우선순위큐4.png)

![우선순위큐](/assets/images/ch-09-우선순위큐5.png)

![우선순위큐](/assets/images/ch-09-우선순위큐6.png)

![우선순위큐](/assets/images/ch-09-우선순위큐7.png)

![우선순위큐](/assets/images/ch-09-우선순위큐8.png)

![우선순위큐](/assets/images/ch-09-우선순위큐9.png)

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF]*(n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a].append((b,c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        # 값이 작다는 것은 이미 처리되어 최소 값이 들어가 있다는 의미
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```
```python  
# 입력 예시
# 1. 노드와 간선 수
# 2. 출발 노드
# 3. 출발노드, 도착노드, 간선 
6 11
1
1 2 2
1 3 5
1 4 1
2 3 3
2 4 2
3 2 3
3 6 5
4 3 3
4 5 1
5 3 1
5 6 2

# 출력 예시
0
2
3
1
2
4
```

### 개선된 다익스트라 알고리즘의 시간 복잡도
* 힙 자료구조를 이용하는 다익스트라 알고리즘의 시간 복잡도는 $O(ElogV)$
  * N = 1,000,000일 때, $log_{2}N$이 약 20인 것을 감안하면 속도가 획기적으로 빨라진다.
* 노드를 하나씩 꺼내 검사하는 반복문(while)은 노드의 개수 V 이상의 횟수로는 처리되지 않는다.
  * 결과적으로 현재 우선순위 큐에서 꺼낸 노드와 연결된 다른 노드들을 확인하는 총횟수는 최대 간선의 개수(E)만큼 연산이 수행될 수 있다.
* 직관적으로 전체 과정은 E개의 원소를 우선순위 큐에 넣었다가 모두 빼내는 연산과 매우 유사하다.
  * 시간 복잡도를 $O(ElogE)$로 판단할 수 있다.
  * 중복 간선을 포함하지 않는 경우에 이를 $O(ElogV)$로 정리할 수 있다 (E가 아무리 많아도 $V^2$를 넘을 수 없음)
    * $O(ElogE)$ -> $O(ElogV^2)$ -> $O(2ElogV)$ -> $O(ElogV)$
    * 통상적으로 간선의 개수 20만 개 이상, 노드 2만 개 이상 이여도 1초 안에 가능

## 플로이드 워셜 알고리즘
* <span style="background-color:#baddfe">모든 노드에서 다른 노드까지의 최단 경로를 모두 계산</span>한다.
* 플로이드 워셜(Floyd-warshall)알고리즘은 다익스트라 알고리즘과 마찬가지로 단계별로 **거쳐 가는 노드를 기준으로 알고리즘을 수행**한다.
  * 다만 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않는다.
* 플로이드 워셜은 2차원 테이블에 최단 거리 정보를 저장한다.
* 가중치가 음수여도 사용이 가능하다.
* 다익스트라 보다 구현은 쉽지만 시간복잡도$O(N^3)$ 
* 플로이드 워셜 알고리즘은 다이나믹 프로그래밍(DP)유형에 속한다.
  * 각 단계마다 **특정한 노드 K를 거쳐 가는 경우를 확인**한다.
    * a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사.
  * 점화식은 $D_{ab} = min(D_{ab},D_{ak}+D_{kb})$

## 플로이드 워셜 알고리즘: 동작 과정

![플로이드워셜](/assets/images/ch-09-플로이드워셜.png)

![플로이드워셜](/assets/images/ch-09-플로이드워셜2.png)

![플로이드워셜](/assets/images/ch-09-플로이드워셜3.png)

![플로이드워셜](/assets/images/ch-09-플로이드워셜4.png)

![플로이드워셜](/assets/images/ch-09-플로이드워셜5.png)

```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 무한으로 초기화
graph = [[INF]*(n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n+1):
    for b in range(1, n+1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
        if graph[a][b] == INF:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()

```
```python  
# 입력 예시
4
7
1 2 4
1 4 6
2 1 3
2 3 7
3 1 5
3 4 4
4 3 2

# 출력 예시
0 4 8 6
3 0 7 9
5 9 0 4
7 11 2 0
```
