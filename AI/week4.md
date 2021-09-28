# Local Search Algorithms(9.23)
* Iterative improvement algorithms
  * 많은 최적화 문제에서, path is irrelevant
    * goal state 자체가 solution인 경우(8-queens problem)
  * State space = set of "complete" configurations
    * Find optimal configuration according to the objective function (TSP)
  * **Complete configuration**으로 시작하고, 퀄리티를 향상하기 위해 조금씩 조정한다
  ![image](https://user-images.githubusercontent.com/68818952/134770845-51a77f4b-dd18-4aa0-9c54-63ea7d67b159.png)
  * global maximum을 찾지 못하고 local maximum에 갇힐 수도 있다 -> 초기 위치에 따라 값이 변동적이다(장단점)

## Hill-climbing Search
* 안개가 자욱하게 낀 에베레스트 산을 등반한다고 생각해보자
  * 감각적으로 증가하는(올라가는) 방향으로만 움직여야 할 것이다 -> Hill Climbing
  * gradiant ascent/descent의 방법이라고 할 수 있다
  ![image](https://user-images.githubusercontent.com/68818952/134770924-7c0f1057-cdbd-4cf6-9fd0-6bafa8f6c471.png)
  * neighbor의 값이 current보다 작으면 즉, 값이 감소하는 구간에 들어간 경우 -> neighbor값이 local max이므로 return
  * 결점 : local maxima에 stop해서 갇혀버린다
  * Possible solution
    * Stochastic hill climbing
      * 통계적으로 방향을 선택 -> 랜덤하게 선택을 하지만 주변 경사도에 따라서 확률을 정하고 랜덤하게 선택
    * First choice hill climbing
      * successor를 랜덤하게 발생하고 좋으면 선택, 나쁘면 버림
      * steepest와 다른점은 steepest는 best만 선택하지만, 랜덤하게 child를 찾아보며 좋은 것이 있으면 이동
    * Random-restart hill climbing
      * 시작하는 위치를 달리한다는 idea. 랜덤하게 초기 시작점을 만들고 그 지점부터 수행하며 maximam 선택
      * 굉장히 효율적이다
  * Complexity
    * state space landscape의 모양에 따라 성공여부가 달려있다.
    * NP-hard 문제가 이러한 문제를 가지고 있다 -> global maxima를 찾는 것은 매우매우 힘들다
    * 차선책으로 생각해 볼 수 있는 것이, 어느정도 괜찮은 local maxima를 찾으면 된다


## Simulated Annealing Search
* gradient descent 또는 valley descending과 random walk의 효율성을 합친 알고리즘이다
* descending은 bad move를 허용함으로써 local minima에서 탈출하는 개념이다
* 계속적으로 bad move를 허용하지는 않는다. **gradually decrease their step size and frequency**
* **Analogy with annealing**
  * 고정된 온도 T, 확률적으로 T에 따라서 움직일 확률 P를 계산할 수 있다
  * T를 천천히 감소시켜가면 -> 항상 best state에 도달하게 된다

![image](https://user-images.githubusercontent.com/68818952/134771570-f7be04ac-f68c-43a1-8e91-c8fc5b034fc0.png)
* 온도 T가 0이면 return.
* 주변 successor를 랜덤하게 선택하고, 그 값과 현재 값과의 차이를 E라고 했을때,
* E가 0보다 작은 경우 -> 감소하는 경우면 minima를 찾기 위한 경우 이므로 최신화 해줌
* E가 0보다 큰 경우 -> bad move (증가하는 경우)를 확률적으로 next로 이동할지 결정한다
* 초반에는 bad move를 허용하다가, 나중에는 점점 good move만 허용 
![image](https://user-images.githubusercontent.com/68818952/134771976-15fa3840-0d49-4fe2-b4b5-79912b022e2c.png)

## Genetic Algorithms
* starts with a population of individuals
  * 각각의 individual의 state는 주로 0, 1로 표현된다
* 각각의 individual은 fitness function에 의해 rated된다 -> 적자생존
  * 계속 나아간다는 용어를 **reproduction** 이라고 한다. fitness score의 확률에 따라 선택됨
* Selected pair are mated by a crossover
![image](https://user-images.githubusercontent.com/68818952/134772677-b73a12d2-9388-4512-99f9-a4ca8b9bdbd7.png)
* 초창기에만 급격한 변화가 발생하고, 시간이 지나면 대부분의 individual이 상태가 비슷해진다
* GA의 장점은 crossover에서 발생한다. crossover 지점도 random하게 잡아야한다
![image](https://user-images.githubusercontent.com/68818952/134772787-17ce0203-c928-421e-ab0e-5ace7489ac1b.png)
![image](https://user-images.githubusercontent.com/68818952/134772870-7b148da8-f298-49ac-8048-d2ecce532153.png)

## Continuous State Spaces(09.28)
* Object function이 함수로 주어졌을 때 연속함수 f가 미분가능 하면 gradiant를 계산할 수 있고, 방향을 따라 이동하면 max, min 방향으로 이동 가능
* gradiant를 구하는 방법
  * 1차 함수이면 미분해서 구하면 되고, 2차 이상의 n차 일때, n개의 편미분을 구해 벡터를 구성하면 된다 -> **벡터의 방향에 집중**
  * gradiant만 구해서 그 방향으로 나아가면 된다
  * **a(알파)는 step size**. a가 너무 작으면 단계가 매우 많아지고, a가 너무 크면 원하는 목표지점을 지나칠 수 있다
  * gradiant f 가 0인 경우 -> 변곡점이 되는 경우이므로 **critical points**가 될 수 있다.

* **Line Search(for min)** : 최적의 a 사이즈를 찾아가는 방법
  * minimize를 한다고 했을 때, x - a * gradinant f 를 계산할 때 a를 여러개를 두어 f값을 가장 작게하는 a 선택
  * 새로운 방향이 선택되어 진다

* gradiant f 가 0인 경우를 바로 찾을 수 있는 경우에는 그 지점으로 바로 가서 max,min 값을 계산하면 된다
  -> 대부분 이런 경우는 존재하기 힘들다.
  
## Constrained Optimization Problem
* Constrained Optimization Problem는 제약조건이 주어진다.
* min f(x)가 있고, x가 n차 벡터라고 하자
  * **gi(x) = 0, i = 1,....,q**
  * **hj(x) <= 0, j = q+1,...,k**
  * **L1 <= xl <=Ul, l = 1,...n**

* Ll과 Ul은 S search space가 정의하는 xl의 상한선 하한선이다.
