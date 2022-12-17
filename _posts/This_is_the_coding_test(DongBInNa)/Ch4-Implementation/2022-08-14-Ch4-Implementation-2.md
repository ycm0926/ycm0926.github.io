---

layout: single
title: "Ch4 Implementation 4-2"
categories: Algorithm
tag: [Python, Algorithm, 이것이 코딩 테스트다]
toc: true
author_profile: false
sidebar:
    nav: "docs"
    
---

## ⚡ [문제 1] 왕실의 나이트

* **난이도: ⭐**
* **풀이 시간: 20분**
* **시간 제한: 1초**
* **메모리 제한: 128MB**

**[문제]**

왕실 정원은 체스판과 같은 8x8 좌표 평면이다. 왕실 정원의 특정한 한 칸에 나이트가 서 있다.
나이트는 말을 타고 있기 때문에 이동을 할 때는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없다. 나이트는 특정한 위치에서 다음과 같은 2가지 경우로 이동할 수 있다.

수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동
수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동

이처럼 8x8 좌표 평면상에서 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 출력하는 프로그램을 작성하시오. 이때 왕실의 정원에서 행 위치를 표현할 때는 1부터 8로 표현하며, 열 위치를 표현할 때는 a부터 h로 표현한다.

**[입력 조건]**

* 첫째 줄에 8x8 좌표 평면상에서 현재 나이트가 위치한 곳의 좌표를 나타내는 두 문자로 구성된 문자열이 입력된다.
* 입력 문자는 a1처럼 열과 행으로 이뤄진다.

**[출력 조건]**

* 첫째 줄에 나이트가 이동할 수 있는 경우의 수를 출력한다.

```python
# 입력 예시
a1

# 출력 예시
2
```


```python
# 1. 나의 풀이

n = input()
print(type(n))
# 인덱싱과 아스키코드를 활용
# dx = direction x, nx = next x
x = ord(n[0]) - 96  # 숫자로 만들어 줌
y = int(n[1])
cnt = 0

dx = [-2, -1, 1, 2, -2, -1, 1, 2]
dy = [1, 2, -2, -1, -1, -2, 2, 1]

for i in range(len(dx)):
	# 이동 후 좌표 구하기
	nx = x + dx[i]
	ny = y + dy[i]

	# 이동 가능할 시 count
	if 0 < nx <= len(dx) and 0 < ny <= len(dy):
		cnt += 1

print(cnt)


# 2. 교재 풀이

input_data = input()
row    = int(input_data[1])
column = int(ord(input_data[0])) - int(ord('a')) + 1

# 나이트가 이동할 수 있는 8가지 방향 정의
steps = [
  (-2, -1), (-2, 1), (2, -1), (2, 1),
  (-1, -2), (1, -2), (-1, 2), (-1, 2)   
        ]
        
  # 8가지 방향에 대하여 각 위치로 이동이 가능한지 확인
  result = 0 
  for step in steps:
  	# 이동하고자 하는 위치 확인
    next_row = row + step[0]
    next_column = column + stpe[1]
    
    # 해당 위치로 이동이 가능하다면 카운트 증가
    if next_row >= 1 and nex_row <= 8 and next_column >= 1 and next_column <= 8 :
        result += 1
    
print(result)

```

## ⚡ [문제 2] 게임 개발

* **난이도: ⭐⭐** 
* **풀이 시간: 40분**
* **시간 제한: 1초**
* **메모리 제한: 128MB**

**[문제]**

게임 캐릭터가 있는 장소는 1x1 크기의 정사각형으로 이뤄진 N x M 크기의 직사각형으로, 각각의 칸은 육지 또는 바다이다. 캐릭터는 동서남북 중 한 곳을 바라본다.

맵의 각 칸은 (A, B)로 나타낼 수 있고, A는 북쪽으로부터 떨어진 칸의 개수, B는 서쪽으로부터 떨어진 칸의 개수이다. 캐릭터는 상하좌우로 움직일 수 있고, 바다로 되어 있는 공간에는 갈 수 없다.

캐릭터의 움직임을 설정하기 위해 정해 놓은 매뉴얼은 아래와 같다.

1. 현재 위치에서 현재 방향을 기준으로 왼쪽 방향(반시계 방향으로 90도 회전한 방향)부터 차례대로 갈 곳을 정한다.

2. 캐릭터의 바로 왼쪽 방향에 아직 가보지 않은 칸이 존재한다면, 왼쪽 방향으로 회전한 다음 왼쪽으로 한 칸을 전진한다. 왼쪽 방향에 가보지 않은 칸이 없다면, 왼쪽 방향으로 회전만 수행하고 1단계로 돌아간다.

3. 만약 네 방향 모두 이미 기본 칸이거나 바다로 되어 있는 칸인 경우에는, 바라보는 방향을 유지한 채로 한 칸 뒤로 가고 1단계로 돌아간다. 단, 이때 뒤쪽 방향이 바다인 칸이라 뒤로 갈 수 없는 경우에는 움직임을 멈춘다.


위 과정을 반복적으로 수행하면서 캐릭터의 움직임에 이상이 있는지 테스트하려고 한다. 매뉴얼에 따라 캐릭터를 이동시킨 뒤에, 캐릭터가 방문한 칸의 수를 출력하는 프로그램을 만드시오.


**[입력 조건]**

* 첫째 줄에 맵의 세로 크기 N과 가로 크기 M을 공백으로 구분하여 입력한다. (3<=N, M<=50)

* 둘째 줄에 게임 캐릭터가 있는 칸의 좌표(A, B)와 바라보는 방향 d가 각각 서로 공백으로 구분하여 주어진다. 방향 d의 값으로는 다음과 같이 4가지로 존재한다.

  * 0 : 북쪽
  * 1 : 동쪽
  * 2 : 남쪽
  * 3 : 서쪽
* 셋째 줄부터 맵이 육지인지 바다인지에 대한 정보가 주어진다. N개의 줄에 맵의 상태가 북쪽부터 남쪽 순서대로, 각 줄의 데이터는 서쪽부터 동쪽 순서대로 주어진다. 맵의 외곽은 항상 바다로 되어 있다.

  * 0 : 육지
  * 1 : 바다

처음에 게임 캐릭터가 위치한 칸의 상태는 항상 육지


**[출력 조건]**

* 첫째 줄에 이동을 마친 후 캐릭터가 방문한 칸의 수

```python
# 입력예시
4 4      # 4x4 맵 생성
1 1 0    # (1,1)에 북쪽(0)을 바라보고 서 있는 캐릭터
1 1 1 1  # 첫 줄은 모두 바다
1 0 0 1  # 둘째 줄은 바다/육지/육지/바다
1 1 0 1  # 셋째 줄은 바다/바다/육지/바다
1 1 1 1  # 넷째 줄은 모두 바다

# 출력예시
3
```


```python
# 1. 나의 풀이

import sys

n, m = map(int, input().split())
x, y, direction = map(int, input().split())

# 이동 가능 모든 경우 북, 동, 남, 서 순서
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
# 바라보는 모든 경우
d_direction = [0, 1, 2, 3]
# 전체 맵 입력
game_map = [list(map(int, input().split())) for _ in range(n)]
# 현재 위치 방문처리
game_map[x][y] = 2
cnt = 1
turn_p = 0
# 맵 이탈 예외
try: 
    while True:
        # 왼쪽 방향으로 회전
        direction = d_direction[direction-1]
        nx = x + dx[direction]
        ny = y + dy[direction]
        # 회전 후 갈 수 있는 곳인지 확인 후 이동
        if game_map[nx][ny] == 0:
            cnt += 1  # 방문 횟수 카운트
            x = nx
            y = ny
            game_map[x][y] = 2  # 방문 기록
            turn_p = 0  # 턴 포인트 0 으로 초기화
            continue
        # 갈수 없는 지역일 경우
        else:
            turn_p += 1
            # 4방향 모두 확인한 경우
            if turn_p == 4:
                nx = x - dx[direction]
                ny = y - dy[direction]
                # 뒤로 갈 수 있다면 이동
                if game_map[nx][ny] != 1:
                    x = nx
                    y = ny
                    turn_p = 0
                # 이동불가 (바다일 경우)
                else:
                    break
except:
    print('맵 이탈')
    exit()
print(cnt)
  

# 2. 교재 풀이

n, m = map(int, input().split())
x, y ,direction = map(int, input().split())

# 방문한 위치 저장용 
d = [[0] * m for _ in range(n)]
d[x][y] = 1

# 전체 맵 정보
array = [list(map(int, input().split())) for _ in range(n)]

# 북, 동, 남, 서 방향 정의
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 왼쪽으로 회전
def turn_left():
  global direction
  direction -= 1
  if direction < 0:
    direction = 3

turn_time = 0 # 회전횟수
count = 1     # 방문횟수

while True:
  turn_left()
  nx = x + dx[direction]
  ny = y + dy[direction]
  if array[nx][ny] == 0 and d[nx][ny] == 0:
    d[nx][ny] = 1
    x, y = nx, ny
    count += 1
    turn_time = 0
    continue
  else:
    turn_time += 1
  if turn_time == 4:
    nx = x - dx[direction]
    ny = y - dy[direction]
    if array[nx][ny] == 0:
      x, y = nx, ny
    else:
      break
    turn_time = 0

print(count)

```

 * 방향을 설정해서 이동하는 문제 유형에서는 dx, dy라는 별도의 리스트를 만들어 방향을 정하는 것이 효과적
 * 2차원 리스트를 선언할 때는 리스트 컴프리헨션을 이용하는 것이 효율적
  
---


## **🍀** 회고
완전탐색 유형과 시뮬레이션 유형에 대해 알아봤다. 그리디와 완전탐색에 비해 어려운 느낌이 들었다. 익숙하지 않은 긴 문제에 차례대로 포인트를 생각하면서 코드로 옮기는 과정이 쉽지가 않았다. 특히나 dx,dy를 이용하여 현재 좌표를 옮기는게 생각보다 어려웠다. 그리고 방문맵 대신 방문시 2를 넣어 체크하여 푸는것도 괜찮은 방법이 아닌가 싶었다. 시뮬레이션은 최하 난이도로 코테 초반 자주 나온다고 하니 많이 풀면서 감을 잡아야 할 거 같다.

