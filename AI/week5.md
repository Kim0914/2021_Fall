# Knowledge Representation (09.30)

* **Ontology**
  * 철학에서는 존재의 본질, 무엇이 진실인지에 관하여 공부하는 분야이다
  * 인공지능에서는 지식 표현의 한 방법이고, 컨셉들간의 관계로 구성되어있는 방법이다
  * 
* **Taxonomic**
  * 실체들은 보통 배열이 가능한데, 계층적인 구조나 taxnomy 구조로 배열할 수 있다
  ![image](https://user-images.githubusercontent.com/68818952/135587749-2e6b0aec-1a1c-44d6-b37c-8d31aae6e616.png)
  * set과 entity의 속성에 대해도 이야기 할 수 있다
  * 모든 동물는 -> skin을 가지고 있다
  * 모든 새는 -> 날 수 있다.
  * 부분집합의 구성원은 상위집합의 속성을 상속받는다
    * 동물들은 피부를 가지고 있따 => 새는 피부를 가지고 있다

* **Sementic Nets**
  * 그래프 구조로 Taxonomic을 표현한 것이다.
  ![image](https://user-images.githubusercontent.com/68818952/135588092-18b1eba0-b464-4f67-9c32-0abcbc24c2c0.png)
  * 직관적으로 그래프를 통해서 나타낼 수 있으므로 효율적이다
  * 노드 : set, entity
  * 세가지 타입의 Edge가 존재한다
    * subset -> superset Edge
    * Entity Edge
    * entity, set -> property Edge
  * Inheritence
    * Subset과 Menmber 링크를 통해서 Property가 상속된다
    * 만약 해당 노드에서 특정 Property에 대해 다른 value가 있어도, 상위 속성을 상속받는다
      * 예를들어, 카나리아가 날수있니? 는 Yes이다
      * 오스트리치는 날수있니? 는 No이다

  * Multiple inheritence
    * 한 물체가 두개이상의 객체를 상속받을 경우, 우선순위를 이용해서 충돌을 방지할 수 있다
    ![image](https://user-images.githubusercontent.com/68818952/135589068-954a861b-b4f4-4ed5-8dcb-9b7f294950e4.png)

  * **한계점**
    * Negation을 표현하기가 어렵다. logic으로는 쉽지만 그래프로는 어렵다
    * Disjunction을 표현하기가 어렵다.
    * Quantification을 표현하기가 어렵다.
    * 따라서 procedual attachment를 도입할 수 있다

  ![image](https://user-images.githubusercontent.com/68818952/135589684-700ac39d-8cac-469d-8f55-7ea2ab010985.png)
  * **이러한 Sementic nets에서 사용하는 데이터 구조를 Frame이라고 한다**
  ![image](https://user-images.githubusercontent.com/68818952/135589823-77ca8f79-7663-4c0a-817a-f28a9c4c8fef.png)


* Nonmonotomic Logic
  * 모노토닉 논리는 '점진적으로 증가한다', '점진적으로 감소한다' 라는 논리이다.
  * 증가하는 경우는 절대 감소하지 않고, 감소하는 경우는 절대 증가하지 않는다
  * Circumscription: 특별한 state가 있지 않는 한, 현재의 조건이 변하지 않고 예상되는 값과 다르지 않다
  * ***명시적으로 기술이 되어있을 때만 적용이 될 수 있다.***
