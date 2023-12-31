# # 알고리즘

## 1. 탐색/자료구조

- **탐색** : 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정, **DFS/BFS**가 대표적인 탐색 알고리즘

- **자료구조** : 데이터를 표현하고 관리하고 처리하기 위한 구조.

## 2. 스택(Stack)/큐(Queue)
#### : 응용은 append 할 때 조건 한 번, pop 하면서도 조건에 맞는 결과를 처리. 즉, 입출입시 총 두 번의 제한을 걸 수 있다고 생각해서 응용하기

- **스택** : 박스 쌓기와 비슷, 선입후출 또는 **후입선출(LIFO)의 선형자료 구조**  

- **큐** : 대기 줄과 비슷, **선입선출(FIFO) 구조(파이썬은 collections 모듈에서 deque 사용)**

## 3. 재귀함수

- **재귀함수** : 자기 자신을 다시 호출하는 함수 → **종료 조건을 꼭 명시해야 함** → **재귀함수는 메모리에서 스택의 형태로 실행됨, 이 원리를 잘 생각해서 사용해야됨**

## 4. DFS(Depth-First Search)

- **깊이 우선 탐색**이라고 부르며, **스택** 자료구조에 기초함. 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
  
  (1) 인접 행렬(Adjacency Matrix) : 2차원 배열로 그래프의 연결 관계를 표현하는 방식
  
  (2) 인접 리스트(Adjacency List) : 리스트로 그래프의 연결 관계를 표현하는 방식
