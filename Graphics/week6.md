# Modeling

* **Polygon Mesh**

  ![image](https://user-images.githubusercontent.com/68818952/136961843-57ebdd39-dd80-482e-a57f-8ffd97730307.png)
  * 컴퓨터로 구를 표현하는 방법: 중점과 반지름을 알고 있다면 구의 방정식을 통해 3차원 구를 표현할 수 있다
  * GPU는 폴리곤을 처리하기에 적합.
  * 표면을 여러개의 점들로 샘플링하고, 각 점들을 vertex라고 하자. 각 점들을 연결해서 만든 것을 Mesh라고 한다
  * 삼각형 Mesh가 자주 사용된다. 사각형 Mesh <-> 삼각형 Mesh
  * 어떤 물체를 모델링 할 때 사용되는 정점의 갯수가 많으면 좀 더 정교하게 표현할 수 있다 (Resolution or Level Of Detail)


* **Polygon Mesh - Not indexed Representation**

  ![image](https://user-images.githubusercontent.com/68818952/136962790-9a258f7a-bd79-4c3d-9bf2-81efca831dfd.png)
  * 삼각형메시로 표현된 물체의 각 정점들은 vertex array에 저장된다
  * 정점을 순서대로 저장한다면 중복되는 데이터가 많아진다 -> t1: (0,1) t2: (0,1)
  * Index array를 구성해서 중복된 데이터를 해결해 메모리를 효율적으로 관리한다
    * 각 메시를 이루는 삼각형의 정점을 순서대로 저장


* **Surface Normals**

  ![image](https://user-images.githubusercontent.com/68818952/136963615-b7d888e3-d8f4-428a-84b4-2c3e9bd80b18.png)
  * 표면 노멀(법선 벡터), 3차원 표면에서 수직으로 밖을 향하는 방향을 나타낸다
  * 삼각형 mesh에서 수직한 방향을 나타낸다. 삼각형에서는 두 방향이 수직으로 존재할 수 있는데, 물체 밖으로 향하는 방향을 말한다
  * 주의할 점은, 계산에서 삼각형 메시의 방향을 반시계방향으로 정의하면 물체 바깥이 아닌 물체 안으로 향하는 벡터가 나옴
  * ***CCW 방향이 매우매우 중요하다 !!***

* Vertex Normals
  
  ![image](https://user-images.githubusercontent.com/68818952/136964528-5f952eb5-db64-4188-9330-41d665a561cf.png)
  * vertex normal은 물체의 표면과 빛의 상호작용을 통해서 분산이나 반사의 효과를 처리하는 기법에 사용됨
  * Vertex에 수직인 방향을 알고싶은데, 특정 정점을 둘러싸고 있는 삼각형 mesh들이 각각의 surface normal을 가지고 있다
    * **그것들의 평균을 구하게 되면 vertex normal이 나오게 된다**

* Export and Import
  * 우리가 만든 3D 모델을 Realtime graphic으로 나타내려면 Export와 Import과정을 거쳐야 한다
  ![image](https://user-images.githubusercontent.com/68818952/136966619-94710f89-0483-4907-9d60-b04f17d869af.png)
