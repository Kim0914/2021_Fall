## 2D -> 3D 변환 (09.30)
* 3D Scaling
  ![image](https://user-images.githubusercontent.com/68818952/135462933-b2b749fb-fb76-4ba6-acde-c92546695963.png)

* 3D Rotation
  * 3차원 로테이션은 2차원이 점을 중심으로 회전하는 것과 달리 **축(axis)을 중심으로 회전한다**
  ![image](https://user-images.githubusercontent.com/68818952/135463306-c3d9f388-7c99-4822-b290-2019ae10affa.png)
  * z축을 기준으로 회전하는 예시이기 때문에 z' 좌표는 변함없다
  * 반시계 방향 회전(Θ > 0)을 Positive라고 보고, 시계 방향 회전(Θ < 0)을 Negative라고 한다.
  
* Translation
  * 2차원에서 했던 것을 z축만 추가한 것과 같다
  ![image](https://user-images.githubusercontent.com/68818952/135465246-de79952b-5c08-4e65-abd6-6a14007b5bb9.png)

## Rotation and Object-space Basis
![image](https://user-images.githubusercontent.com/68818952/135471480-9fb49dc3-8ed4-4c8e-b321-c9c300d9bb48.png)
* 물체가 만들어지면, object space에 고정된다.
* object-space의 basis 벡터는 {u, v, n} 이다
* world-space의 basis 벡터는 {e1, e2, e3} 이다
* (u, v, n) = R(e1, e2, e3) 라고 생각할 수 있다 -> world-space 기저벡터가 로테이션 행렬과 곱해져서 나온 벡터


## Inverse of Translation and Scaling
![image](https://user-images.githubusercontent.com/68818952/135472817-51243335-3d59-4e7d-a3ef-0f46899b0a2b.png)
* 원상태로 돌아오기 위해서는 역으로 빼주면 되기 때문에, dx = -dx, dy = -dy, dz= -dz
* 2배만큼 scaling 했으면, 1/2만큼 Scaling 곱해주면 다시 원래대로 돌아온다.

## Inverse Rotation
![image](https://user-images.githubusercontent.com/68818952/135473649-382c864c-0980-4c23-9bfc-7ac0df919c4b.png)
* u, v, n 도 orthonormal basis이다. 따라서 **u·u = v·v = n·n = 1** and **u·n = v·n = n·u = 0**
* 대각행렬만 1이고 나머지가 0인 Identity Matrix I가 나온다.
* **R^T * R = I이므로, R^-1 = R^T이다**
