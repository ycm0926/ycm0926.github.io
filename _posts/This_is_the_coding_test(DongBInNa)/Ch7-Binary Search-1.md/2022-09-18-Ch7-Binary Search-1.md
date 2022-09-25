---

layout: single
title: "Ch7 Binary Search 7-1"
categories: Algorithm
tag: [python, coding, algorithm, 이것이 코딩 테스트다]
toc: true
author_profile: false
sidebar:
    nav: "docs"

---


# 📚 순차 탐색(Sequential Search) 알고리즘

**순차 탐색 (Sequential Search)** 이란 <span style="background-color:#baddfe">리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인하는 방법</span>
* 보통 정렬되지 않은 리스트에서 데이터를 찾을 때 사용
* 리스트 내에 데이터가 아무리 많아도 시간만 있다면 원하는 데이터를 찾을 수 있다는 장점
* 데이터 개수가 N개일 때 최대 N번의 비교 연산이 필요하므로 최악의 경우 시간복잡도 O(N)

```python
def sequential_search(n, target, array):
    for i in range(n):
        if array[i] == target:
            return i + 1

input_data = input().split()
n = int(input_data[0])
target = input_data[1]

array = input().split()

print(sequential_search(n, target, array))
```

# 📚 이진 탐색(Binary Search) 알고리즘

**이진 탐색 (Binary Search)** 이란 <span style="background-color:#baddfe">정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법</span>
* 이진 탐색은 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정
* 퀵 정렬(quick_sort)과 비슷하게 탐색 범위를 절반씩 좁혀가며 데이터를 탐색
* 데이터를 한번 확인할때마다 원소의 개수가 절반씩 감소한다는 점에서 시간 복잡도가 O(logN)
* 이진탐색을 구현하는 방법에는 2가지(재귀함수, 반복문)

## **1) 재귀함수**
```python
# 재귀함수 호출
'''
10 7
1 3 5 7 9 11 13 15 17 19
'''
def binary_search_recursive(array, target, start, end):
    if start > end:
        return None

    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    elif array[mid] > target:
        return binary_search_recursive(array, target, start, mid-1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else:
        return binary_search_recursive(array, target, mid+1, end)

# n(원소의 개수)과 target(찾고자 하는 문자열)을 입력받기
n, target = list(map(int, input().split()))
# 전체 원소 입력받기
array = list(map(int, input().split()))
result = binary_search_recursive(array, target, 0, n-1)

# 이진 탐색 수행 결과 출력
if result == None:
    print('찾는 값이 없습니다.')
else:
    print(result + 1)
```
**실행결과**
```python
10 7 ⮐
1 3 5 7 9 11 13 15 17 19 ⮐
4

10 7 ⮐
1 3 5 6 9 11 13 15 17 19 ⮐
원소가 존재하지 않습니다
```
## **2) 반복문**
```python
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
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid + 1
    return None

# n(원소의 개수)과 target(찾고자 하는 값)을 입력 받기
n, target = list(map(int, input().split()))
# 전체 원소 입력 받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)
```
**실행결과**
```python
10 7 ⮐
1 3 5 7 9 11 13 15 17 19 ⮐
4

10 7 ⮐
1 3 5 6 9 11 13 15 17 19 ⮐
원소가 존재하지 않습니다
```
## **코딩 테스트 에서의 이진 탐색**
* 이진 탐색은 코딩 테스트에서 단골로 나오므로 가급적 외우길 권함(참고할 소스코드가 없는 상태에서는 이진 탐색의 구현이 상당히 어려울 수 있음)
* 탐색 범위가 2000만이 넘어가면 이진 탐색으로 문제에 접근하길 권함
  * 1000만 단위 이상으로 넘어가면 이진 탐색과 같이O(logN)의 속도를 내야 하는 알고리즘을 떠올려야 문제를 풀 수 있는 경우가 많다.

**이진 탐색과 순치 탐색 비교**
![이진vs순차](/assets/images/이진vs순차.gif)

# 📚 트리 자료구조
* 노드와 노드의 연결로 표현하며 여기에서 노드는 정보의 단위로서 어떠한 정보를 가지고 있는 개체로 이해할 수 있다.
* 큰 데이터를 처리하는 소프트웨어는 대부분 데이터 트리 자료구조로 저장해서 이진탐색과 같은 탐색 기법을 이용해 빠르게 탐색이 가능하다.

## 트리의 특징
![트리](/assets/images/트리.png)
>* 트리는 부모 노드와 자식 노드의 관계로 표현한다.
>* 트리의 최상단 노드를 루트 노드라고 한다.
>* 트리의 최하단 노드를 단말 노드라고 한다.
>* 트리에서 일부를 떼어내도 트리 구조이며 이를 서브 트리라고 한다.
>* 트리는 파일 시스템과 같이 계층적이고 정렬된 데이터를 다루기에 적합하다.

## 이진 탐색 트리
![이진트리](/assets/images/이진트리.png)

트리 자료구조 중에서 가장 간단한 형태가 이진 탐색 트리이다.
이진 탐색 트리 : 이진 탐색이 동작할 수 있도록 고안된, 효율적 탐색이 가능한 자료구조
부모 노드보다 왼쪽 자식 노드가 작다.
부모 노드보다 오른쪽 자식 노드가 크다

빠르게 입력받기
Python input() 함수는 동작 속도가 느리다.
한 줄 입력받고 rstrip() 함수를 꼭 호출해야 한다.


binary search (반으로 쪼개면서 탐색하기)
배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있다.
데이터가 무작위일때는 사용할 수 없다.
탐색 범위를 절반씩 좁히면서 데이터를 탐색하는 특징이 있다.
이진 탐색은 변수 3개를 사용하여 구현하는데 변수는 시작점, 끝점, 중간점을 사용한다.
찾으려는 데이터와 중간점(middle) 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는다.
시작점과 끝점, 중간점을 정할 때 중간점이 실수일 때는 소수점 이하를 버린다.
시간 복잡도가 O(logN)이다.
절반씩 데이터를 줄어들도록 만든다는 점에서 퀵 정렬과 공통점이 있다.
이진 탐색을 구현하는 방법은 2가지가 있다.
1) 재귀 함수를 이용한 구현
2) 반복문을 이용한 구현
코딩 테스트에서 이진 탐색 문제는 탐색 범위가 큰 상황에서 탐색을 가정하는 문제가 많다
탐색(data) 범위가 2000만을 넘어가면 이진 탐색으로 접근해보자
  
---
