---

layout: single
title: "Ch3 Greed Algorithm 3-2"
categories: Algorithm
tag: [python, coding, algorithm, 이것이 코딩 테스트다]
toc: true
author_profile: false
sidebar:
    nav: "docs"

---


## ⚡ [문제 2] 숫자 카드 게임

* **난이도: ⭐**
* **시간 제한: 1초**
* **메모리 제한: 128MB**
* **기출: 2019 국가 교육기관 코딩 테스트**

**[문제]**

숫자 카드 게임은 여러 개의 숫자 카드 중에서 가장 높은 숫자가 쓰인 카드 한 장을 뽑는 게임이다.
단, 게임의 룰을 지키며 카드를 뽑아야 하고 룰은 다음과 같다.

* 숫자가 쓰인 카드들이 N x M 형태로 놓여 있다. 이때 N은 행의 개수를 의미하며, M은 열의 개수를 의미한다.
* 먼저 뽑고자 하는 카드가 포함되어 있는 행을 선택한다.
* 그다음 선택된 행에 포함된 카드들 중 가장 숫자가 낮은 카드를 뽑아야 한다.
* 따라서 처음에 카드를 골라낼 행을 선택할 때, 이후에 해당 행에서 가장 숫자가 낮은 카드를 뽑을 것을 고려하여 최종적으로 가장 높은 숫자의 가드를 뽑을 수 있도록 전략을 세워야 한다.
  
카드들이 N x M 형태로 놓여 있을 때, 게임의 룰에 맞게 카드를 뽑는 프로그램을 만드시오.

**[입력 조건]**

* 첫째 줄에 숫자 카드들이 행의 개수 N과 열의 개수 M이 공백을 기준으로 하여 각자 자연수로 주어진다. (1 <= N, M <= 100)
* 둘째 줄부터 N개의 줄에 걸쳐 각 카드에 적힌 숫자가 주어진다. 각 숫자는 1 이상 10,000 이하의 자연수이다.

**[출력 조건]**

* 첫째 줄에 게임의 룰에 맞게 선택한 카드에 적힌 숫자를 출력한다.
  
```python
# 입력 예시 1
3 3
3 1 2
4 1 4
2 2 2

# 출력 예시 1
2
```
```python
# 입력 예시 2
2 4
7 3 1 8
3 3 3 4

# 출력 예시 2
3
```
```python
# 1. 나의 풀이

N, M = map(int, input().split())

ans = 0

for i in range(N):
    arr = list(map(int, input().split()))
    min_arr = min(arr)
    ans = max(min_arr, ans)
    
print(ans)


# 2. 교재 풀이 (시간복잡도 O(N)) 

n,m = map(int,input().split())
result = 0

for i in range(n):
  data = list(map(int,input().split()))
  result = max(result, min(data))  # min(), max() 함수를 이용해서 찾는 방식
  print(result)

```
