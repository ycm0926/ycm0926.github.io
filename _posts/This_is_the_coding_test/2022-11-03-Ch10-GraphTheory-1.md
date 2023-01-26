---

title: "Ch10 Graph Theory 10-1"
categories: Algorithm
tag: [Python, Algorithm, 이것이 코딩 테스트다]
toc: true
toc_sticky: true
author_profile: true
sidebar:
    nav: "docs"

---

# 📚 복습

**DFS/BFS**와 **최단경로**는 그래프 알고리즘의 한 유형 이며 이외에도 그래프 알고리즘은 굉장히 다양한데, 코딩 테스트에서 출제 비중이 낮지만 꼭 알아야 하는 알고리즘이다. 10장에서 다룰 알고리즘은 앞서 배운 내용에 기반한다.
* 크루스칼 알고리즘(Kruskal Algorithms): 그리디 알고리즘의 한 유형
* 위상 정렬 알고리즘(Topology Algorithms): 큐 자료구조 or 스택 자료구조를 활용해 구현

>📌알고리즘 문제를 접했을 때 알아두어야 할 점
> * '서로 다른 개체(혹은 객체)가 연결되어 있다'는 이야기는 가장 먼저 그래프 알고리즘을 떠올려야 한다. 
>   * 예를들어 '여러 개의 도시가 연결되어 있다'와 같은 내용이 등장하면 그래프 알고리즘을 의심해보자.

그래프 자료구조 중에서 트리(Tree) 자료구조는 다양한 알고리즘에서 사용되므로 꼭 기억.
* 트리 자료구조는 부모 -> 자식으로 내려오는 계층적인 모델이다.
* 트리는 수학에서는 무방향 그래프로 간주하지만, 컴퓨터공학 분야에서는 방향 그래프로 간주한다.

![그래프트리](/assets/images/ch10/ch-10-그래프트리.png)

앞서 그래프의 구현 방법에는 2가지가 있다고 했다. 두 방식은 메모리와 속도 측면에서 구별된다.

* 인접 행렬(Adjacency Matrix): 2차원 배열을 사용하는 방식
  * 간선 정보를 저장하기 위해 O(V²)만큼의 메모리 공간 필요
  * 특정 노드 A에서 다른 특정 노드 B로 이어진 간선의 비용을 O(1) 시간으로 즉시 알 수 있다.
  * 플로이드 워셜 알고리즘은 인접 행렬을 이용
    * 모든 노드에 대해 다른 노드로 가는 최소 비용을 V² 크기의 2차원 리스트에 저장한 뒤에, 해당 비용을 갱신해서 최단 거리를 계산

* 인접 리스트(Adjacency List): 리스트를 사용하는 방식
  * 간선의 개수만큼인 O(E)만큼만 메모리 공간 필요
  * 특정 노드 A에서 다른 특정 노드 B로 이어진 간선의 비용을 알려면 O(V)만큼의 시간이 소요된다.
  * 우선순위 큐를 이용하는 다익스트라 최단 경로 알고리즘은 인접 리스트를 이용
    * V개의 리스트를 만들어서 각 노드와 연결된 모든 간선에 대한 정보를 리스트에 저장

>📌알고리즘 선택시 알아두어야 할 점
>* **메모리와 시간을 염두에 두고 알고리즘을 선택해서 구현해야 한다.**
>   * 예를 들어, 최단 경로를 찾아야하는 문제가 있을 때, 노드의 개수가 적은 경우에는 플로이드 워셜 알고리즘을, 노드와 간선의 개수가 많은 경우에는 우선순위 큐를 사용하는 다익스트라 알고리즘을 사용하면 유리하다.

# 📚 서로소 집합 (Disjoint Sets) 알고리즘

**서로소 집합** (Disjoint Sets)란 <span style="background-color:#baddfe">공통 원소가 없는 두 집합</span>을 의미한다.

![서로소집합](/assets/images/ch10/ch-10-서로소집합.png)

* 서로소 집합 자료구조란 <span style="background-color:#baddfe">서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조</span>라고 할 수 있다.
* 서로소 집합 자료구조는 두 종류의 연산을 지원한다.
  * **합집합(Union)**: 두 개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산이다.
  * **찾기(Find)**: 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산이다.
* 서로소 집합 자료구조는 **합치기 찾기(Union Find) 자료구조** 라고 불리기도 한다.
  
## 서로소 집합 자료구조
* 여러 개의 합치기 연산이 주어졌을 때 서로소 집합 자료구조의 동작 과정은 다음과 같다.
  1. 합칩합(Union) 연산을 확인하여, 서로 연결된 두 노드 A, B를 확인한다.  
  
     1) A와 B의 루트 노드 A', B'를 각각 찾는다.  
     2) A'를 B'의 부모 노드로 설정한다.

  2. 모든 합집합(Union) 연산을 처리할 때까지 1번의 과정을 반복한다.  
* 합집합 연산 시 일반적으로 큰 루트 노드가 작은 루트 노드를 따르는 것이 관행적이다.

## 서로소 집합 자료구조: 동작 과정 살펴보기

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정.png)

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정2.png)

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정3.png)

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정4.png)

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정5.png)


## 서로소 집합 자료구조: 연결성
* 서로소 집합 자료구조에서는 **연결성**을 통해 손쉽게 집합의 형태를 확인할 수 있다.

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정6.png)

* 기본적인 형태의 서로소 집합 자료구조에서는 루트 노드에 즉시 접근할 수 없다.
  * 루트 노드를 찾기 위해 <U>부모 테이블을 계속해서 확인</U>하며 거슬러 올라가야 한다.

![서로소동작과정](/assets/images/ch10/ch-10-서로소동작과정7.png)

## 서로소 집합 자료구조: 구현 방법
```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
  # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
  if parent[x] != x:
    return find_parent(parent, parent[x])
  return x

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
  a = find_parent(parent, a)
  b = find_parent(parent, b)
  if a < b:
    parent[b] = a
  else:
    parent[a] = b

# 노드의 개수와 간선(union 연산)의 개수 입력받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v+1):
	parent[i] = i

# Union 연산을 각각 수행
for i in range(e):
	a, b = map(int, input().split())
  union_parent(parent, a, b)
 
# 각 원소가 속한 집합 출력
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
  print(find_parent(parent, i), end=' ')

print()

# 부모 테이블 내용 출력
print('부모 테이블: ', end='')
for i in range(1, v + 1):
  print(parent[i], end=' ')
```
```python
#입력 예시
6 4
1 4
2 3
2 4
5 6

#출력 예시
각 원소가 속한 집합: 1 1 1 1 5 5
부모 테이블: 1 1 2 1 5 5
```

## 서로소 집합 자료구조: 기본적인 구현 방법의 문제점
* 합집합(Union) 연산이 편향되게 이루어지는 경우 찾기(Find) 함수가 비효율적으로 동작함
* 최악의 경우에는 찾기(Find) 함수가 모든 노드를 다 확인하게 되어 시간 복잡도가 O(V)
  * 다음과 같이 {1, 2, 3, 4, 5]의 총 5개의 원소가 존재하는 상황을 확인했을 경우
  * 수행된 연산들: Union(4,5), Union(3,4), Union(2,3), Union(1,2)

![서로소동작문제점](/assets/images/ch10/ch-10-서로소동작문제점.png)

## 서로소 집합 자료 구조: 경로 압축
* 찾기(Find) 함수를 최적화하기 위한 방법으로 경로 압축(Path Compression)을 이용할 수 있음
  * 찾기(Find) 함수를 재귀적으로 호출한 뒤에 <u>부모 테이블 값을 바로 갱신</u>

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```

* 경로 압출 기법을 적용하면 각 노드에 대하여 찾기(Find) 함수를 호출한 이후에 해당 노드의 루트 노드가 바로 부모 노드가 됨
* 동일한 예시에 대해서 모든 합집합(Union) 함수를 처리한 후 각 원소에 대하여 찾기(Find) 함수를 수행하면 다음과 같이 부모 테이블이 갱신
* 기본적인 방법에 비하여 시간 복잡도가 개선됨
  
![서로소동작문제점](/assets/images/ch10/ch-10-서로소동작문제점2.png)

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화히기

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i

# Union 연산을 각각 수행
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)

# 각 원소가 속한 집합 출력하기
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, 1), end=' ')

print()

# 부모 테이블 내용 출력하기
print('부모 테이블: ', end='')
for i in range(1, v + 1):
    print(parent[i], end=' ')
```
```python
#입력 예시
6 4
1 4
2 3
2 4
5 6

#출력 예시
각 원소가 속한 집합: 1 1 1 1 5 5
부모 테이블: 1 1 1 1 5 5 
```

## 서로소 집합 알고리즘의 시간 복잡도
* 경로 압축 방법만을 사용하며 노드의 개수가 v, 최대 v-1개의 union 연산과 m개의 find 연산이 가능하면
* 시간 복잡도는 $O(V + M(1+log_{2-M/V}V))$이다.
* 더 짧은 방법도 존재하지만 코테 수준에서 경로 압축만 적용해도 충분하며 개념 및 구현 간단하다.

## 서로소 집합을 활용한 사이클 판별
* 서로소 집합은 **무방향 그래프 내에서의 사이클을 판별**할 때 사용할 수 있다.
  * 참고로 방향 그래프에서의 사이클 여부는 DFS를 이용하여 판별할 수 있다.(해당 내용은 책에서 다루지 않는다)
* **사이클 판별 알고리즘**은 다음과 같다.
  1. 각 간선을 하나씩 확인하며 두 노드의 루트 노드를 확인한다.  
   
     1) 루트 노드가 서로 다르다면 두 노드에 대하여 합집합(Union) 연산을 수행한다.   
     2) 루트 노드가 서로 같다면 사이클(Cycle)이 발생한 것이다.
   
  2. 그래프에 포함되어 있는 모든 간선에 대하여 1번 과정을 반복한다.

## 서로소 집합을 활용한 사이클 판별: 동작 과정 살펴보기

![서로소사이클](/assets/images/ch10/ch-10-사이클.png)

![서로소사이클](/assets/images/ch10/ch-10-사이클2.png)

![서로소사이클](/assets/images/ch10/ch-10-사이클3.png)

![서로소사이클](/assets/images/ch10/ch-10-사이클4.png)


```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화히기

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i

cycle = False # 사이클 발생 여부

for i in range(e):
    a, b = map(int, input().split())
    # 사이클이 발생한 경우 종료
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    # 사이클이 발생하지 않았다면 합집합(Union) 연산 수행
    else:
        union_parent(parent, a, b)

if cycle:
    print("사이클이 발생했습니다.")
else:
    print("사이클이 발생하지 않았습니다.")
```
```python
#입력 예시
3 3
1 2
1 3
2 3

#출력 예시
사이클이 발생했습니다.
```


# 📚 신장트리 (Spanning Tree)
* <u>그래프가 있을 때 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프</u>를 의미한다.
  * 모든 노드가 포함되어 연결되면서 사이클이 존재하지 않는다는 조건은 트리의 성립 조건이기도 하다.

![신장트리](/assets/images/ch10/ch-10-신장트리.png)
* 신장 트리가 아닌 부분은 1번 노드가 포함되어 있지 않으며, 사이클이 존재한다.

---
* **<u>최소한의 비용으로 구성되는 신장 트리를 찾아야 할 때</u> 어떻게 할까?**
* 예를 들어 N개의 도시가 존재하는 상황에서 두 도시 사이에 도로를 놓아 **전체 도시가 서로 연결**될 수 있는 도로를 설치하는 경우를 생각한다.
  * 두 도시 A, B를 선택했을 때 A에서 B로 이동하는 경로가 반드시 존재하도록 도로를 설치

![최소신장트리](/assets/images/ch10/ch-10-최소신장트리.png)

## 크루스칼 알고리즘
* 대표적인 **최소 신장 트리 알고리즘**
* 그리디 알고리즘으로 분류
* 트리의 자료구조이므로 간선의 개수는 '노드의 개수-1'과 같다.
* 구체적인 동작 과정은 다음과 같다.
  1. 간선 데이터를 비용에 따라 **오름차순으로 정렬**
  2. 간선을 하나씩 확인하며 <u>현재의 간선이 사이클을 발생시키는지 확인</u>한다.  
  
     1) 사이클이 발생하지 않는 경우 최소 신장 트리에 포함한다.  
     2) 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않는다.

  3. 모든 간선에 대하여 2번의 과정을 반복한다.

## 크루스칼 알고리즘: 동작 과정

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작2.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작3.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작4.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작5.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작6.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작7.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작8.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작9.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작10.png)

![크루스칼](/assets/images/ch10/ch-10-크루스칼동작11.png)

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        parent[x] = find_parent(parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(a, b):
    a = find_parent(a)
    b = find_parent(b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 모든 간선을 담을 리스트와, 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블 상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i

# 모든 간선에 대한 정보를 입력 받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫번째 원소를 비용으로 설정
    edges.append((cost, a, b))

# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
    if find_parent(a) != find_parent(b):
        union_parent(a, b)
        result += cost

print(result)
```
```python
#입력 예시
7 9
1 2 29
1 5 75
2 3 35
2 6 34
3 4 7
4 6 23
4 7 13
5 6 53
6 7 25

#출력 예시
159
```

## 크루스칼 알고리즘: 성능 분석
* 크루스칼 알고리즘은 간선의 개수가 E개일 때, O(ElogE)의 시간 복잡도를 가진다.
* 왜냐하면 크루스칼 알고리즘에서 가장 많은 시간을 요구하는 것은 간선의 정렬을 수행하는 부분이다.
  * 표준 라이브러리를 이용해 E개의 데이터를 정렬하기 위한 시간 복잡도는 O(ElogE)

# 📚 위상 정렬 (Topology Sort)
* <span style="background-color:#baddfe">사이클이 없는 방향 그래프의 모든 노드를 '방향성에 거스르지 않도록 순서대로 나열하는 것'</span>을 의미
* 예시) 선수과목을 고려한 학습 순서 설정

![위상정렬](/assets/images/ch10/ch-10-위상정렬.png)

* 위 세 과목을 모두 듣기 위한 **적절한 학습 순서**는?
  * 자료구조 -> 알고리즘 -> 고급 알고리즘 <span style="color:blue">(O) 
  * 자료구조 -> 고급 알고리즘 -> 알고리즘 <span style="color:red">(x)</span>

## 진입차수와 진출차수
* 진입차수(Indegree): 특정한 노드로 들어오는 간선의 개수
* 진출차수(Outdegree): 특정한 노드에서 나가는 간선의 개수

![진입차수 진출차수](/assets/images/ch10/ch-10-진입차수와진출차수.png)

## 위상 정렬 알고리즘
* **큐**를 이용하는 **위상 정렬 알고리즘의 동작 과정**은 다음과 같다. (DFS로도 가능)
  1. 진입차수가 0인 모든 노드를 큐에 넣는다.  
  2. 큐가 빌 때까지 다음의 과정을 반복한다.   
    1). 큐에서 원소를 꺼내 해당 노드에서 나가는 간선을 그래프에서 제거한다.  
    2). 새롭게 진입차수가 0이 된 노드를 큐에 넣는다.

-> 결과적으로 **각 노드가 큐에 들어온 순서가 위상 정렬을 수행한 결과**와 같다.

## 위상 정렬 알고리즘: 동작 과정

* 위상 정렬을 수행할 그래프를 준비
  * 이때 그래프는 사이클이 없는 방향 그래프 (DAG)여야 한다.

![위상동작예시](/assets/images/ch10/ch-10-위상정렬동작예시.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작2.png)
* 본 예제는 더 작은 번호의 노드가 우선으로 큐에 들어가게끔 가정

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작3.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작4.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작5.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작6.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작7.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작8.png)

![위상정렬동작](/assets/images/ch10/ch-10-위상정렬동작9.png)

## 위상 정렬 알고리즘: 특징
* 위상 정렬은 DAG에 대해서만 수행할 수 있다.
  * **DAG (Direct Acyclic Graph)**: 순환하지 않는 방향 그래프
* 위상 정렬에서는 여러 가지 답이 존재할 수 있다.
  * 한 단계에서 큐에 새롭게 들어가는 원소가 2개 이상인 경우가 있다면 **여러 가지 답이 존재**할 수 있다.
* **모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재**한다고 판단할 수 있다.
  * 사이클에 포함된 원소 중에서 어떠한 원소도 큐에 들어가지 못한다.
* 스택을 활용한 DFS를 이용해 위상 정렬을 수행할 수도 있다.

```python
from collections import deque

# 노드의 개수와 간선의 개수를 입력 받기
v, e = map(int, input().split())
# 모든 노드에 대한 진입차수는 0으로 초기화
indegree = [0] * (v + 1)
# 각 노드에 연결된 간선 정보를 담기 위한 연결 리스트 초기화
graph = [[] for i in range(v + 1)]

# 방향 그래프의 모든 간선 정보를 입력 받기
for _ in range(e):
    a, b = map(int, input().split())
    graph[a].append(b) # 정점 A에서 B로 이동 가능
    # 진입 차수를 1 증가
    indegree[b] += 1

# 위상 정렬 함수
def topology_sort():
    result = [] # 알고리즘 수행 결과를 담을 리스트
    q = deque() # 큐 기능을 위한 deque 라이브러리 사용
    # 처음 시작할 때는 진입차수가 0인 노드를 큐에 삽입
    for i in range(1, v + 1):
        if indegree[i] == 0:
            q.append(i)
    # 큐가 빌 때까지 반복
    while q:
        # 큐에서 원소 꺼내기
        now = q.popleft()
        result.append(now)
        # 해당 원소와 연결된 노드들의 진입차수에서 1 빼기
        for i in graph[now]:
            indegree[i] -= 1
            # 새롭게 진입차수가 0이 되는 노드를 큐에 삽입
            if indegree[i] == 0:
                q.append(i)
    # 위상 정렬을 수행한 결과 출력
    for i in result:
        print(i, end=' ')

topology_sort()
```
```python
#입력 예시
7 8
1 2
1 5
2 3
2 6
3 4
4 7
5 6
6 4

#출력 예시
1 2 5 3 6 4 7
```
## 위상 정렬 알고리즘: 성능 분석
* 위상 정렬을 위해 차례대로 모든 노드를 확인하며 각 노드에서 나가는 간선을 차례대로 제거해야 함
  * 위상 정렬 알고리즘의 시간 복잡도는 O(V + E)
