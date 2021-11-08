# Extended operators of relational algebra

## Bags
### Bag이란 무엇일까?
* 일반적으로 데이터베이스의 각종 데이터들은 간단한 순수 집합 베이스의 tuple이다.
* 가끔, DBMS의 Relation은 Duplicate Tuple이 허용된다.
  * **즉, 같은 tuple(record)가 1회 이상 반복된다는 것**
* 이 반복되는 tuple이 있는 Table set을 **Bag** 또는 **Multiset**이라고 부른다
* Set과 Bag 모두 집합의 의미이며, Table 내에서 tuple(record)의 순서는 상관 없다

### Bag을 사용하는 이유
* 개념적으로는 중복을 허용하지 않아 tuple 개수가 더 적은 Set이 Bag보다 빠르고 효율적인 것 처럼 보인다
  * **set 연산을 통해 결과를 얻은 경우, tuple 하나씩 모두 비교해서 중복을 확인해야 하기 때문에**
* **Union 연산이나 Projection 연산의 경우 bag이 굉장히 효율적이다.**

### Union, Intersection, Difference of Bag
![image](https://user-images.githubusercontent.com/68818952/139588752-cc325759-e876-4cb2-b029-c80f45150e92.png)

* Relation R에 Tuple T가 n개, Relation S에 Tuple T가 m개 있을 경우
* T의 개수 #T
  * #T in (R U S) = n+m
  * #T in (R n S) = MIN(n,m)
  * #T in (R - S) = MAX(0, n-m)


### Algebra Laws for Bags(연산법칙)
![image](https://user-images.githubusercontent.com/68818952/139588916-6dd1e42a-2ae9-4fd7-9b51-3a3045fe7d26.png)
* 교환법칙의 경우 Set, Bag 둘다 성립한다
* 하지만 분배법칙의 경우 성립하지 않는다.

### Product of Bags
![image](https://user-images.githubusercontent.com/68818952/139589041-42d4e4f5-b09b-4fcc-af74-a49ab465b9fe.png)
* Set의 Product 연산과 같다.
* R에 tuple T1이 n개, S에 tuple T2가 m개 있을 때 Product R X S 에 tuple T1T2가 nm번 나온다

## Join of Bags
![image](https://user-images.githubusercontent.com/68818952/139589054-08adbd4b-e38e-4c98-83d4-d248f4784c8d.png)
* Join 연산도 마찬가지로 Set과 다르지 않다.
* 조건에 맞는지 비교하고 결과 튜플을 작성하면 된다.
* **연산 중 중복을 제거하지 않는다**
* **즉, 각각 별개의 독립적인 튜플로 취급**

## Duplication Elimination
![image](https://user-images.githubusercontent.com/68818952/140755465-21146353-53fa-482a-8b06-c95713140862.png)
* 말 **그대로 중복을 제거하는 연산**
* 델타로 표현하며, Bag인 R의 중복튜플들을 제거함으로써 Set으로 변환

## Aggregation Operators
![image](https://user-images.githubusercontent.com/68818952/140756405-831387ce-ffb5-484a-ae56-5d5a42cef61a.png)
* 결과를 **특정 연산을 취함으로써 하나의 결과로 반환**
 * SUM: Column의 SUM값을 반환한다
 * AVG: Column의 Average값을 반환한다
 * COUNT: Column의 Count값을 반환한다
 * MIN and MAX: 가장 작은 값과 가장 큰 값을 반환한다

## Grouping
* 보통 전체 컬럼을 가지고 Average 같은 aggregation 연산을 하지 않는다
* 각각 컬럼 1개 전체의 연산 말고, **좀 더 컬럼들을 묶어서 연산을 한다**
  * 예를 들어, Studio마다 상영시간의 총합을 알고 싶은 경우
    * Studio마다 묶어서 상영시간의 총합 Group마다 독립적으로 계산
* yL(R) 감마로 표현하며, List L: Attribute 및 Aggregation으로 나타낸다
* 이 때, 그룹화의 기준이 되는 컬럼을 Grouping Attribute, Aggregation 연산을 하는 컬럼을 Aggregated attribute라고 한다
* yL(R)의 특징
  * **R의 일부를 Group화 한다**. 각 그룹들은 Grouping attribute에 해당하는 1개의 값을 갖는 모든 Tuple들로 구성 **(중복제거)**
  * 만약 Grouping attribute가 없다면, Relation R은 1 Group이다
  * L에는 Attribute, 연산, ->(Renaming)등을 기재할 수 있다
  * L에는 연산이 들어가면, 각 Group당 1개의 tuple만 존재하게 된다

## Special case of gamma
* 델타는 여러가지 표현이 존재한다.
* 예를들어, R(A,B,C)에 대해 델타(R) = 감마A,B,C(R)이다.
* 즉 델타는 Aggregation 없이 모든 컬럼들을 각각 그룹화 하는 것과 같다
* 그럼 각각의 Group들은 감마 연산자 자체가 중복을 제거하기 때문에 결국 같아진다
* 하지만 델타는 더 일반적이고 중요한 연산자라 Algebraic 측면에선 더욱 고려할 필요가 있다

## Outerjoin
![image](https://user-images.githubusercontent.com/68818952/140761270-55078ddd-ddd1-4faf-8b71-095cf9fd1f47.png)
* 원래 Join 연산은 주어진 조건을 만족하는 tuple만 반환하는 연산이었다
* OuterJoin은 조건에 부합하지 않는 Tuple들 전부도 처리해주는 연산이다 -> NULL값들을 ㅗ기호로 표시한다
