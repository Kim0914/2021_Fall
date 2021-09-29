# Relation Model (09.29)
![image](https://user-images.githubusercontent.com/68818952/135225476-ba655ac6-d74f-4699-9446-969f2df880b3.png)
* UML, ER모델을 배웠고 오늘은 Relation Model
* Relation is **a kind of Table**
* A1, A2, ... An을 Atrribute라고 한다
* m1은 attribute value라고 한다
* m1,m2,m3...,mn 한줄을 record 또는 tuple이라고 한다

## Relation Schema
* ***relation schema***
  * Relation name
  * attributes, in order
    * Example: Beers(name, manufacture) or Beers(name:string, manf:string)
  * Key definition
  * Primary key에는 underline을 한다
  * Any additional constraints

* Example
  * Schema: Movie(title, year, length, genre)

## Why Relational Model
1. 매우 간단한 모델
2. 우리가 데이터에 생각한대로 매치할 수 있다
3. 관계형 모델과 SQL은 가장 널리 쓰이고 중요하다
