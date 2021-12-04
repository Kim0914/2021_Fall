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
* NOT NULL: 해당 속성이 절대 NULL값을 가질 수 없다는 것.
* DEFAULT <value>: 해당 속성의 input값이 없으면 자동적으로 기본값 value가 들어감.
```SQL
  CREATE TABLE Drinkers(
    name CHAR(20) PRIMARY KEY,
    addr CHAR(40) DEFAULT '123 Sesame St.',
    phone CHAR(16) NOT NULL
  );
```
  
## Inserting a Tuple
* INSERT INTO statement to insert a record into a table
