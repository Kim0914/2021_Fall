# Informed Search Strategies and Local Search Algorithms (9.16)

## Informed Search Strategies
1. Greedy Best-first Search
2. A Search

### **Evaluation function f(n)** = 노드 n에서 goal 까지의 distance
  * 100프로 정확하지는 않다.
  * 최대한 그럴싸한 함수를 도출해야한다
* f(n)이 사용되는 곳은 Priority queue에서 Priority 담당
* f(n) = g(n) + h(n)
  * h(n) = estimated cost of the cheapest path from node n to the goal
  * Heuristic function h(n)은 좋으면 좋을수록 좋지만, 제일 좋고 이런것은 없다

### Greedy Best-first Search
* Expands the node cloest to the goal
  * f(n) = h(n)
    * Evaluate noeds by using just the heuristic funtion
  * Takes the biggest bite possible -> the name **"Greedy Search"**
  * 과거는 생각하지 않고 현재 상태에서 가장 좋은 곳을 신경쓴다고 하면 f(n) = h(n)
  * 미래는 생각하지 않고, 왔던 길만 신경쓴다고 하면 uniform-cost search f(n) = g(n)
    * g does not direct search toward the goal (목표에 대한 정보를 주지 않음)
  * h(n)이 존재하는 경우만 informed search 라고 할 수 있다
  * ***즉, 얼마가 좋은 heuristic function을 찾느냐가 중요 !!***
    * Hsld(n) = straight-line distance between n and the goal location

![image](https://user-images.githubusercontent.com/68818952/133575415-214f9c70-c347-4aff-8e18-81a9e04e8b95.png)

1. 초기 상태 Arad(366) 선정
2. Frontier node에서 popout 한 후, 가장 거리가 짧은 Sibiu(253) 선택
3. Sibiu를 탐색할 때, Arad가 다시 나왔음으로 redundant path 허용 -> Tree search best
4. 그러나 greedy 알고리즘에서 다시 redundant하게 방문할 일은 거의 없다
5. Fagaras(176)를 선택한 후 확장

![image](https://user-images.githubusercontent.com/68818952/133575889-8d751775-6da7-4efc-a31f-6a6faf68a58d.png)

6. Fagaras를 Frontier node에서 popout
7. Bucharest 까지 가는 path 발견 -> goal 도달

* Greedy Best-first Search 평가
  * Optimal 하지 않고 finite space에서 완벽하지 않다
    * Redundant path가 존재하여 Infinite loop가 생길 수 있다
  * Time and space complexity
    * Retains all leaf nodes in memory
    * O(b^m), m : maximum depth of the search space
    * Good heuristic function can reduce the space and time complexity
  * finite space에서 Greedy best-first **graph** search는 complete하다


### A Search
* Minimizes the total estimated solution cost
* Combination of ***greedy best-first search*** and ***uniform-cost search***
  * f(n) = g(n) + h(n)
    * g(n) : path cost from the start node to n
    * h(n) : estimated cost of the cheapest path from n to the goal
    * f(n) : estimated cost of the cheapest solution through n

* A Search는 uniform-cost search와 거의 동일하다
* 다른점은 g 대신에 g+h를 사용한다는 것
* Tree search 기반
  ![image](https://user-images.githubusercontent.com/68818952/134769573-ef1780f7-b84c-4121-ae2f-f48b64111806.png)
  ![image](https://user-images.githubusercontent.com/68818952/134769577-4a2b9601-eda6-48af-b46d-4d5cd7aa2c40.png)
  ![image](https://user-images.githubusercontent.com/68818952/134769599-5b417d7a-88f0-4c7f-972a-0863f6ec9579.png)

* Graph search 기반
* ![image](https://user-images.githubusercontent.com/68818952/134769733-8cafe80a-8ad0-4747-b19b-0eb79e3213ac.png)

* Theorem (Tree-Search case)
 * A* tree search는 h(n)이 goal에 도달하는 비용보다 크지 않을때만 optimal하다 (h(n) is admissible)

* Theorem (Graph-Search case)
 * The graph-search version of A* is Optimal if h(n) is consistent
 * A* graph search는 h(n)이 admissible 하다면 optimal을 보장하지 못한다
 * frontier가 optimal solution이 되는 node를 포함하지 않을 것이기 때문에
 * A* graph search의 optimal을 위해서는 **consistency**라는 더 강력한 조건이 필요하다
  * ![image](https://user-images.githubusercontent.com/68818952/134770093-e624e158-a03a-48ca-94bc-ffefc57fb4df.png)
  * 삼각형에서 두 변의 길이의 합은 가장 긴 변의 길이보다 크다는 공식과 일맥상통

* Evaluation
 * A* is **optimal and complete**
 * Time and meomory complexity
  * Exponetial time complexity
   * Perfect h -> no search (parctically impossible)


* Recall that f(n) = g(n) + h(n)
 * h = 0 -> uniform cost search
 * g = 1, h = 0 -> breadth-first search
 * g = 0 -> greedy best-first search
