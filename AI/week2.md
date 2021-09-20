## Uniform-cost Search (9.14)
* Expand the least-cost unexpanded node on the fronier rather than the shallowest node
  * => 가장 얕은 노드가 아닌, 가장 cost가 적은 노드부터 탐색
* Graph search based
  * Frontier is a **Priority queue** -> lowest first
* 기본적으로는 redundant path 제거하지만, 한시적으로는 허용할 수 있다
* Tree search based 도 가능하지만, 효과적이지는 않다
* **가장 낮은 cost의 solution을 찾는 것이 목표이다**

![image](https://user-images.githubusercontent.com/68818952/133918195-69fcf274-eaee-492f-aad5-f93121bd830d.png)
1. Frontier : S         Path : 
2. Frontier : (A,1), (B,5), (C,15)    Path : S
3. Frontier : (B,5), (C,15)           Path : S - A - G (11 , X)
* 여기서 S - A - G 의 루트로 goal 까지의 Path가 완성이 되는데 lowest cost solution이 아니다.
* 즉, 노드의 generation 시점에서 goal test를 하면 안된다. Frontier node에 들어가서 선택될 때 goal test를 해야한다
4. Frontier : (B,5), (C,15), (G,11)   Path : S - A
5. Frontier : (C,15), (G,10)          Path : S - B
6. Frontier : (C,15)                  Path : S - B - G (10, O)
* 여기서 S - A - G 의 cost 11보다, S - B - G 의 cost 10이 더 적으므로 G 선택

## Depth-fist Search
* Frontier is a stack, put successors at front
  * The 1st node on the frontier is the deepest unexpanded node
  * => 가장 먼저 선택되는 노드는, 가장 deep한 노드가 선택된다
* Tree search based
* 무한루프를 반드시 피해야한다.
  * => path를 거쳐오는 과정에서 다시 똑같은 ancestor 노드를 만나게 되면 버린다 
* Modest memory requirement
* Recursion을 이용해 알고리즘 구현
* Graph search based로 구현하면 explored set의 크기가 exponential하게 커지므로 의미 X
* 메모리적으로는 장점이 있지만, 시간적으로는 단점이 있다

![image](https://user-images.githubusercontent.com/68818952/133918781-9e67bb6f-da94-489a-b4ef-23a062f25204.png)


## Depth-limited Search
* Equal to the depth-first search with depth-limit l
  * 노드가 depth l 에 도달하게 되면 진행하지 않음
  * 일반적으로 tree search
* 어느정도 limit을 잡는 것이 좋을까?
  * 범위를 알 수 있으면 좋은데, 이것이 힘들다
* Evalution
  * Take O(b^l) time
  * Take O(b*l) space
  * d <= l 이면 solution을 찾을 수 있지만, d > l 이면 찾을 수 없다


## Iterative Deepening Search
* depth를 0부터 무한히 증가시킨다
* DFS와 BFS를 적절하게 섞어서 사용하는 알고리즘

![image](https://user-images.githubusercontent.com/68818952/133919636-f71e76dc-ff69-457d-956e-f461c090291f.png)

* **F에서 O까지 가는 최소거리의 path를 구해보자**
* Limit = 0 => cutoff
* Limit = 1 => F ->[B, E, J, G] -> cutoff
* Limit = 2 => F -> B -> [A, C] -> cutoff
* Limit = 2 => F -> E -> [A, I] -> cutoff
* Limit = 2 => F -> G -> [C, H, K] -> cutoff
* Limit = 2 => F -> J -> [I, K, N] -> cutoff
* ***Limit = 3 => F -> G -> K -> O -> solution return***
* Evaluation
  * Optimal and complete like BFS
  * Modest memory like DFS
  * BFS보다 살짝 느리다
  * Take O(b^d) time and O(b*d) space
