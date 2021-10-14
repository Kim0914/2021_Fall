# Vertex Processing
## GPU Rendering Pipeline
![image](https://user-images.githubusercontent.com/68818952/137285067-0a25481e-2e39-4a9d-bf14-cf0713ed9b4c.png)

* 지피유를 이용해서 3차원 폴리곤 메시로 된 것을 2차원 폴리곤 메시로 나타낸다
* vertex shader, frament shader는 SW라고 보면 되고 rasterizer, output merger는 HW라고 보면 된다
* **Vertex shader**
  * vertex shader로 수행되는 연산 중에서, 가장 필수적인 것은 정점에 연속된 변환을 적용시키는 것이다
  * object space -> world space -> camera space -> clip space
  * object space -> world space 과정인 world transform은 4과에서 배웠다 !
  * 이번 주차에는 view transform과 projection transform을 배울 것이다
  * world transform을 Vertex shader에 적용하면 안된다 => normalize 했을 경우 수직 벡터가 되지 않을 수 있다

* **View Transform**

  ![image](https://user-images.githubusercontent.com/68818952/137287085-e346e580-897e-4e7c-802c-ff33894899a2.png)
  * EYE: world space에서 카메라가 위치하는 좌표
  * AT: 카메가 어떤 장면을 찍기 위해서는, 그 장면을 위해 방향을 틀어야하는데 카메라가 향하고 있는 reference point
  * UP: 카메라의 상단이 향하는 방향. 보통의 경우 world space상에서 y축을 말한다
  * n: 카메라가 바라보는 반대 방향의 단위 벡터
  * u: UP 벡터와 n벡터가 이루는(cross product에 의해) 평면에 수직한(orthonormal) 벡터
  * v: n과 u를 cross product한 벡터. 단위 벡터들을 cross product했기 때문에 normalize 하지 않아도 된다. v와 UP이 동일하지 않을 수 있다
  * ***Carmera space는 {u,v,n,EYE} 벡터로 이루어진 공간이고, {u,v,n}은 카메라 공간의 orthonormal basis이다
