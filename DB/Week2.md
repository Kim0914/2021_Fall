# Database 

## Two different aspects of DB
![image](https://user-images.githubusercontent.com/68818952/132472151-23d72ff1-63e7-4b6a-9bf4-ee9e4d259943.png)

* Applications : Applications are developed on the conceptual understanding of real world
* Logical Representation : how to conceptually understand and describe information -> Database issue
* Physical Representation : something of implementation part, how to phsically organize data in file systems -> DBMS issue(phase 2)
* 로지컬과 애플리케이션의 관계는 로지컬을 기반으로 애플리케이션을 개발하는 것
* 애플리케이션은 로지컬을 기반으로 하는  추가적인 층이다


## Three Level Schema of Databases
![image](https://user-images.githubusercontent.com/68818952/132472179-0d3f2987-a85e-4837-b061-d11327124530.png)

* Applications : **External level** (schema)
* Logical Representation : **Conceptual level** (schema)
* Physical Representation : **Physical level** (schema)
* ***Logical Representation Layer는 Physical Representation에 Independent하다***

### DB관련된 job 인터뷰에서 가장 자주 나오는 질문이 위의 2개의 관한 내용이다

---
# Data Modelling
* Object-Modeling Technique (OMT)
  * James Rumbaugh Object-Oriented Modeling and Design
  * Then it has been unified into UML in 1999

## What is a Class Diagram?
* A class diagram describes
  * the type of objects in the system
  * the various kinds of static relationships that exist among them
  * A grphical representation of a static view on declarative static elements
* A central modeling technique that runs through nearly all objected-oriented methods
* The ricehst notation in UML

## Essential Element of a UML Class Diagram
* **Class**
* **Attributes**
* Operations
* **Relationships**
  * Association
  * Generalization
  * Dependency
  * Realization


* Constraint Rules and Notes
