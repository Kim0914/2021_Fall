## 2D Transformation
  * Scaling
    * x축으로 확대, y축으로 확대
    ![image](https://user-images.githubusercontent.com/68818952/135214116-69676b4c-e273-47d7-b3fe-68200aa2e62c.png)
 
  * Rotation
    * 평면상의 임의의점 p=(x,y), 반지름이 r인 원 위의 점으로 표현하면 xcosθ, ysinθ
    ![image](https://user-images.githubusercontent.com/68818952/135214740-202d3131-8c2b-4671-b351-1826ada1ee06.png)
    * **R(θ)는 θ만큼 회전했을 때 rotation matrix**

  * Translation
    * 좌표상의 x,y가 있을 때 x',y' = (x+dx, y+dy) 벡터의 연산으로 나타낸다
    * 이 변환을 **matrix translation**으로 나타낼 수도 있다
    ![image](https://user-images.githubusercontent.com/68818952/135215332-091d8f92-31bb-47d6-bfcd-f3f4ea164e7d.png)
    * 동차 좌표계에서는 (x,y,1)만 쓰는 것이 아니고, (wx,wy,w)등 0이 아닌 w로도 나타낼 수 있다
    * 예를들어 (2,3)은 동차 좌표계로 (2,3,1), (4,6,2), (6,9,3)다 가능하다 -> 방향은 일정

## Homogeneous Coordinates


## Rigid transfformation and affine transformation
