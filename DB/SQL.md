## Why SQL?
* SQL은 very-high-language이다.
* Procedual Language: C, C++, ....
* Declartive Language: Prologut, **SQL**
* Data Definition: Table을 만드는 기능, 주로 CREATE를 사용한다.
* DATA Manipulation: Insert, Delete...

## Declaring a Relation
  ```SQL
  CREATE TABLE Name(
    id INT PRIMARY KEY,
    name CHAR(10)
  );

  DROP TABLE Name;
  ```
 
## Elements of Table Declarations
* INT, INTEGER
* REAL, FLOAT
* CHAR(N) = fixed length string of n charaters
* VARCHAR(n) = variable length string of up to n charaters
* SQL은 대소문자 구별하지 않지만 스타일을 맞추는 것이 좋다.
* Dates and Times
  * DATE: 'yyyy-mm-dd', TIME: 'hh:bb:ss'

## Declaring Keys
* Attribute는 PRIMARY KEY or UNIQUE로 설정될 수 있다 -> 아무것도 선언되지 않을 수도 있음 !
```SQL
CREATE TABLE Beers(
  name CHAR(20) UNIQUE, // 유니크라고 반드시 키 X
  manf CHAR(20)
);
```
* PRIMARY KEY에 대해서 DBMS는 index를 제공한다.
* Key가 2개 이상의 속성을 가질 때에도 사용할 수 있다.
```SQL
CREATE TABLE Sells(
  bar CHAR(20),
  beer VARCHAR(20),
  price REAL,
  PRIMARY KEY (bar, beer)
);
```

## PRIMARY KEY vs UNIQUE
* DBMS는 자료를 찾기 위해 PRIMARY KEY에 index를 제공한다. UNIQUE는 index가 제공되지 않는다.
* 하나의 Realtion에는 하나의 PRIMARY KEY가 있고, UNIQUE는 여러개 존재할 수 있다.
* PRIMARY KEY는 절대 NULL이 올 수 없고, UNIQUE는 NULL값이 올 수 있다.

## Other Declarations for Attributes
* NOT NULL: 해당 속성이 절대 NULL값을 가질 수 없다는 것. Default는 기본값으로 value 값을 넣는다는 것.
```SQL
  CREATE TABLE Drinkers(
    name CHAR(20) PRIMARY KEY,
    addr CHAR(40) DEFAULT '123 Sesame St.',
    phone CHAR(16) NOT NULL
  );
```

## Inserting a Tuple
* INSERT INTO statement to insert a record into a table
```SQL
 CREATE TABLE Drinkers(
    name CHAR(20) PRIMARY KEY,
    addr CHAR(40) DEFAULT '123 Sesame St.',
    phone CHAR(16) NOT NULL
  );
  
  INSERT INTO Drinkers (name, addr, phone)
  VALUES ('Kim Dong Uk', 'Pusan 123', '010-1234-5678');
```
  
## Adding attribute
* We may change a relation schema by **adding a new attribute**("column") by
```SQL
  ALTER TABLE Bars ADD
    phone CHAR(16) DEFAULT 'unlisted';
```
  
## Deleting attribute
* Remove an attribute from a relation schema by 
```SQL
  ALTER TABLE Bars
    DROP license;
```
## Views
* View is a **'virtual table'**, a relation that is defined in terms of the contents of other tables and views
* 기존에 있는 Table에서 조건에 만족하는 것들로 다시 Table을 만드는데, **기본적으로는 가상의 테이블**이다.
* 실제로 조건에 만족하는 테이블을 복사하고 싶으면 'MATERIALIZE VIEW'를 사용하면 된다.
```sql
  CREATE VIEW CanDrink AS
    SELECT drinker, beer // 필요한 것
    FROM Frequents, Sells // 테이블
    WHERE Frequents.bar = Sells.bar; // 조건
```
* View의 좋은 점은 복잡한 쿼리를 이해하기 쉽게 표현할 수 있다는 점이다.
* Select, From, Where 구문을 Relation algebra인 Projection, Selection, Join으로 표현할 수 있다.
* 이 과정은 DBMS가 효율적으로 알아서 처리한다. 

## Data Manipulation: Select-From-Where Statements
* 전형적인 쿼리의 형태는 다음과 같다
```sql
SELECT desired attribute
FROM one or more tables
WHERE condition about tuples of the tables
```
* Beers(name, manf), what beers are made by OB?
```sql
SELECT name
FROM Beers
WHERE manf = 'OB';
```

## * IN SELECT clauses
* FROM 부분에 relation이 하나만 있는 경우, SELECT * 을 할 수 있다.
* 이렇게 하면 테이블의 모든 속성이 출력된다.
* Using Beers(name, manf)
```sql
SELECT *
FROM Beers
WHERE manf='OB';
```

## Renaming Attributes
* 만약 결과로 나오는 속성의 이름을 **다른 이름으로 바꾸고 싶다면 "AS new name** 을 사용해라
```sql
SELECT name AS beer, manf // name을 beer로 바꾼다. manf에는 영향 x
FROM Beers
WHERE manf = 'OB';

Using Sells(bar,beer,price)
SELECT bar, beer, price * 120 AS priceInYen // 수식도 가능하다
FROM Sells;
WHRER X // WHERE 조건이 없으면 모든 record 출력


Using Likes(drinker, beer)
SELECT drinker, 'likes Cass' As whoLikesCass // 결과로 나오는 테이블의 속성은 drinker, whoLikesCass
FROM Likes
WHERE beer = 'Cass'; // whoLikeCase의 value는 'likes Cass'
```

## Patterns
* WHERE 절에서 문자열 일부를 비교할 수 있다.
* 일반적인 형태는 LIKE, NOT LIKE를 이용하여 비교한다.
* % = any string, _ = any character
```sql
Using Drinkers(name, addr, phone) find the drinkers with 555 of phone number
SELECT name
FROM Drinkers
WHERE phone LIKE '%555-_ _ _ _';
```

## NULL Values
* NULL을 사용하는 2가지의 경우가 있다.
  * 하나는, Missing value 즉, 값을 모르는 경우. 예를 들어 내가 그 사람의 배우자에 대한 정보를 모르는 경우
  * 두번째는, Inapplicalge 즉, 적용할 수 없는 경우. 예를 들어 배우자를 찾는데 미혼인 사람은 배우자가 없다 
* NULL에 비교해서 3가지의 logic value가 있다.
  * 1. TRUE: 1의 값을 가진다
  * 2. FALSE: 0의 값을 가진다
  * 3. UNKNOWN: 1/2의 값을 가진다
* AND = MIN, OR = MAX, NOT: 1-x
* Example
  * TRUE AND (FALSE OR NOT(UNKNOWN))
  * = MIN(1, (MAX(0, 1-1/2))
  * = MIN(1, MAX(0, 1/2))
  * = MIN(1, 1/2)
  * = 1/2 (UNKNOWN)

(ppt 36p 까지 정리)
