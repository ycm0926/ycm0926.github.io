---

title: "Ch7 Binary Search 7-2"
categories: Algorithm
tag: [Python, Algorithm, 이것이 코딩 테스트다]
toc: true
toc_sticky: true
author_profile: true
sidebar:
    nav: "docs"

---

## ⚡ [문제 1] 부품찾기

* **난이도: 🌕🌗**
* **풀이시간: 30분**
* **시간 제한: 1초**
* **메모리 제한: 128MB**


**[문제]**

동빈이네 전자 매장에는 부품이 N개 있다. 각 부품은 정수 형태의 고유한 번호가 있다. 어느 날 손님이 M개 종류의 부품을 대량으로 구매하겠다며 당일 날 견적서를 요청했다. 동빈이는 때를 놓치지 않고 손님이 문의한 부품 M개 종류를 모두 확인해서 견적서를 작성해야 한다. 이때 가게 안에 부품이 모두 있는지 확인하는 프로그램을 작성해보자.

**[예시]**
```python
N = 5
[8, 3, 7, 9, 2]

# 손님은 총 3개의 부품이 있는지 확인 요청했는데 부품 번호는 다음과 같다.
M = 3
[5, 7, 9]
```

**[입력 조건]**

* 첫째 줄에 정수 N이 주어진다. (1 <= N <= 1,000,000)
* 둘째 줄에는 공백으로 구분하여 N개의 정수가 주어진다. 이때 정수는 1 보다 크고 1,000,000 이하이다.
* 셋째 줄에는 정수 M이 주어진다. (1 <= M <= 100,000)
* 넷째 줄에는 공백으로 구분하여 M개의 정수가 주어진다. 이때 정수는 1 보다 크고 1,000,000 이하이다.
출력

**[출력 조건]**

* 첫째 줄에 공백으로 구분하여 각 부품이 존재하면 yes를, 없으면 no를 출력한다.

```python  
# 입력 예시
5
8 3 7 9 2
3
5 7 9

# 출력 예시
no yes yes
```

**[문제 해설]**

* 다량의 데이터 검색을 요구하는 문제이므로 이진 탐색 알고리즘을 이용한다.
* 부품을 정렬한 뒤 정렬된 부품들을 이진 탐색을 수행한다.
* 부품을 찾는 과정에서 최악의 경우 O(M*logN)의 연산이 필요하므로 이론상 최대 약 200만 번의 연산이 이루어진다고 볼 수 있다.
* 부품을 정렬하기 위해서 요구되는 시간 복잡도 O(N*logN)이 이론적으로 최대 약 2,000만 번이 연산이 필요하다고 볼 수 있다.
* 결론적으로 이진 탐색을 사용하는 문제 풀이 방법의 경우 시간 복잡도는 **O((M+N)*logN)** 이다.
* 이 문제의 경우 3가지 방법의 솔루션이 있다.

**1. 반복문**
```python

# 교재 풀이

# 이진 탐색 소스코드 구현 (반복문)
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # 찾은 경우 중간점 인덱스 반환
        if array[mid] == target:
            return mid
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid - 1
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 오른쪽 확인
        else:
            start = mid + 1
    return None

# N(가게의 부품 개수) 입력
n = int(input())
# 가게에 있는 전체 부품 번호를 공백을 기준으로 구분하여 입력
array = list(map(int, input().split()))
array.sort() # 이진 탐색을 수행하기 위해 사전에 정렬 수행
# M(손님이 확인 요청한 부품 개수) 입력
m = int(input())
# 손님이 확인 요청한 전체 부품 번호를 공백을 기준으로 구분하여 입력
x = list(map(int, input().split()))

# 손님이 확인 요청한 부품 번호를 하나씩 확인
for i in x:
    # 해당 부품이 존재하는지 확인
    result = binary_search(array, i, 0, n - 1)
    if result != None:
        print('yes', end=' ')
    else:
        print('no', end=' ')

```
**2. 계수 정렬**

```python

# 교재 풀이

# N(가게의 부품 개수) 입력
n = int(input())
array = [0] * 1000001

# 가게에 있는 전체 부품 번호를 입력 받아서 기록
for i in input().split():
    array[int(i)] = 1

# M(손님이 확인 요청한 부품 개수) 입력
m = int(input())
# 손님이 확인 요청한 전체 부품 번호를 공백을 기준으로 구분하여 입력
x = list(map(int, input().split()))

# 손님이 확인 요청한 부품 번호를 하나씩 확인
for i in x:
    # 해당 부품이 존재하는지 확인
    if array[i] == 1:
        print('yes', end=' ')
    else:
        print('no', end=' ')

```
**3. 집합 자료형 이용**
  * 단순히 특정한 수가 한 번이라도 등장했는지를 검사하면 된다.
  * 소스코드가 간결한 측면에서 가장 우수 

```python

# 교재 풀이

# N(가게의 부품 개수) 입력
n = int(input())
# 가게에 있는 전체 부품 번호를 입력 받아서 집합(Set) 자료형에 기록
array = set(map(int, input().split()))

# M(손님이 확인 요청한 부품 개수) 입력
m = int(input())
# 손님이 확인 요청한 전체 부품 번호를 공백을 기준으로 구분하여 입력
x = list(map(int, input().split()))

# 손님이 확인 요청한 부품 번호를 하나씩 확인
for i in x:
    # 해당 부품이 존재하는지 확인
    if i in array:
        print('yes', end=' ')
    else:
        print('no', end=' ')

```


## ⚡ [문제 2] 떡볶이 떡 만들기

* **난이도: 🌕🌕**
* **풀이시간: 40분**
* **시간 제한: 2초**
* **메모리 제한: 128MB**


**[문제]**

동빈이네 떡볶이 떡은 길이가 일정하지 않다. 대신에 한 봉지 안에 들어가는 떡의 총 길이는 절단기로 잘라서 맞춰준다. 절단기에 높이(H)를 지정하면 줄지어진 떡을 한 번에 절단한다. 높이가 H보다 긴 떡은 H위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않는다.

예를 들어, 높이가 19, 14, 10, 17 cm인 떡이 있고 절단기 높이를 15cm로 지정하면 자른 뒤 떡의 높이는 15, 14, 10, 15cm가 될 것이다. 그리고 잘린 떡의 길이는 차례대로 4, 0, 0, 2cm가 된다. 이 때 손님은 잘린 떡의 길이의 총 합인 6cm의 길이를 가져간다.

손님이 왔을 때 요청한 총 길이가 M일 때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하시오

**[입력 조건]**

* 첫째 줄에 떡의 개수 N과 요청한 떡의 길이 M이 주어진다(1 <= N <= 1,000,000, 1 <= M <= 2,000,000,000)
둘째 줄에는 떡의 개별 높이가 주어진다.

* 떡 높이의 총합은 항상 M 이상이므로 손님은 필요한 양만큼 떡을 사갈 수 있다. 높이는 10억보다 작거나 같은 양의 정수 또는 0이다.(0 <= H <= 10억)

**[출력 조건]**

* 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력한다.

```python  
# 입력 예시
4 6
19 15 10 17

# 출력 예시
15
```

**[문제 해설]**

* 적절한 높이를 찾을 때까지 이진 탐색을 수행하여 높이 H를 반복하여 조정하면 된다

* '현재 이 높이로 자르면 조건을 만족할 수 있는가?'를 확인한 뒤에 조건의 만족 여부('예' 혹은 '아니오')에 따라서 탐색 범위를 좁혀서 해결할 수 있다

* 절단기의 높이는 0부터 10억까지의 정수 중 하나이다
  * 이렇게 큰 탐색 범위를 보면 가장 먼저 이진 탐색을 떠올려야 한다

문제에서 제시된 예시를 통해 그림으로 이해해 보자

[Step 1] 시작점: 0, 끝점: 19, 중간점: 9 이때 필요한 떡의 크기: M = 6이므로, 결과 저장
![떡볶이1](/assets/images/algorithm/ch7/ch-07-떡볶이1.png)
[Step 2] 시작점: 10, 끝점: 19, 중간점: 14 이때 필요한 떡의 크기: M = 6이므로, 결과 저장
![떡볶이2](/assets/images/algorithm/ch7/ch-07-떡볶이2.png)
[Step 3] 시작점: 15, 끝점: 19, 중간점: 17 이때 필요한 떡의 크기: M = 6이므로, 결과 저장
![떡볶이3](/assets/images/algorithm/ch7/ch-07-떡볶이3.png)
[Step 4] 시작점: 15, 끝점: 16, 중간점: 15 이때 필요한 떡의 크기: M = 6이므로, 결과 저장
![떡볶이4](/assets/images/algorithm/ch7/ch-07-떡볶이4.png)

* 이러한 이진 탐색 과정을 반복하면 답을 도출할 수 있다
* 중간점의 값은 시간이 지날수록 '최적화된 값'이 되기 때문에, 과정을 반복하면서 얻을 수 있는 떡의 길이 합이
필요한 떡의 길이보다 크거나 같을 때마다 중간점의 값을 기록하면 된다


```python
# 교재 풀이

import sys
# 떡의 개수 N과 요청한 떡의 길이 M 입력 받기
n, m = map(int, sys.stdin.readline().rstrip().split())
# 각 떡의 개별 높이 입력 받기
n_list = list(map(int, sys.stdin.readline().rstrip().split()))

# 이진 탐색을 위한 시작점과 끝점 설정
start = 0
end = max(n_list)

# 이진 탐색 수행(반복적)
result = 0

while (start <= end):
    total = 0
    # 절단기 높이 지정
    mid = (start+end)//2
    # 잘랐을 때의 떡의 양 계산
    for n in n_list:
        # 떡의 높이가 더 높을 때만 자를 수 있음
        if (n > mid):
            total += n - mid

    # 떡의 양이 부족한 경우 더 많이 자르기(왼쪽 부분 탐색)
    if (total < m):
        end = mid - 1
    # 떡의 양이 충분한 경우 덜 자르기(오른쪽 부분 탐색)
    else:
        result = mid # 최대한 덜 잘랐을 때가 정답이므로, 여기에서 result에 기록
        start = mid + 1

print(result)

```
* 전형적인 이진 탐색의 문제이자, 파라메트릭 서치(parametic search) 유형의 문제이다. 파라메트릭 서치는 **최적화 문제를 결정 문제로 바꾸어 해결하는 기법이다.** 
  * '원하는 조건을 만족하는 가장 알맞은 값을 찾는 문제'에 주로 파라메트릭 서치를 사용한다. 
  * 결정 문제는 ‘예' 혹은 ‘아니오'로 답하는 문제를 말한다.
* 예를들어 범위 내에서 조건을 만족하는 가장 큰 값을 찾는 최적화 문제라면 이진 탐색으로 결정 문제를 해결하면서 좁혀갈수 있다.
* 따라서, 해당 문제에선, ‘현재 이 높이로 자르면 조건을 만족할 수 있는가?”를 확인한 뒤, 조건의 만족 여부(’예' 혹은 ‘아니오')에 따라서 탐색 범위를 좁혀서 해결할 수 있다.
* 코테나 프로그래밍 대회에서 보통 파라메트릭 서치 유형은 이진 탐색을 이용하여 해결한다.
* 절딘가 범위가 1부터10억이며 이처럼 큰 수를 보면 당연하듯 가장 먼저 이진탐색을 떠올려야한다.

---

## **🍀** 회고
이진 탐색이 알고리즘적으로는 이해는 했지만 이를 코드로 구현하기엔 앞서 배운 DFS, BFS처럼 상당히 어렵다. 다음에 이진 탐색 문제들도 많이 접하면서 익숙해져야겠다.
