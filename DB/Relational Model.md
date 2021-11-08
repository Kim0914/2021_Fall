## Relational Operator
1. Union
2. Intersection
3. Difference
4. Select: 테이블에서 원하는 Tuple을 추출한다. 예를 들어 score>3.5(Student) -> Closed operation
5. Project: 테이블에서 원하는 속성값들을 추출한다. 예를 들어 name(score>3.5(Student)) -> Not closed operation
6. Cartesian Product
7. Join

## Constraint on Relation
1. Referential constraints: Student -> Department 관계가 있다고 했을 때, Student의 dept는 반드시 Department의 name에 존재해야함
2. Key Constraint: 한 Object에서 Key값이 동일하면 다른 값도 모두 동일해야 한다.

## UML -> Relational Model
* Class to Relational Model
  * 그냥 하면 된다
* Association
  * One-way association
    * Person -> Company의 관계에서 Company의 Cardinality가 1인 경우 Person Table에 Company의 PK를 집어 넣는다
  * Two-way association
    * Person -> Company의 관계에서 Company의 Cardinality가 1..*인 경우 두 Relation 사이의 새로운 Table을 만든다
    * 새로 만든 Contract라는 테이블에 Person의 Key와 Company의 Key 모두 다 들어가야 함

* Aggregation
  * One-way이든 Two-way이든 동일하게 표현
  * Country -> Department의 관계가 1..* -> 1..1 이라고 했을 때 Deparatment내에 Country가 belongs to 이므로
  * Country TABLE에 belongsToDept CHAR(30)으로 관계를 표현한다

* Inheritance
  * 상속관계에서는 Sub class가 Super class의 Attribute를 모두 상속한다.
  * Sub class에서 PK를 Super class의 Key 중에서 PK를 선택하는 것이 좋다

* Weak Entity Set
  * Weak Entity Set은 Table 하나로 Key를 만들지 못한다.
  * Player -> Football team의 관계에서 Player의 테이블에 Football team의 Key인 teamName 선언
  * 이후 PK (backnumber, TeamName)으로 설정한다
