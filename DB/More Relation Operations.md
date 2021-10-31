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
