# Definitions of computer graphics
* The study of **creating**, **manipulating**, and **using visual images** in the computer
* Using a computer as a rendering tool for the generation and manipulation of images is called ***computer graphics***
* More precisely : **image synthesis**
* 컴퓨터 그래픽스의 3가지 요소
  1. Modeling
  2. Rendering
  3. Animation


* **컴퓨터 그래픽스**와 **이미지 프로세싱**의 차이점 
  * 이미지 프로세싱은 생성된 기존의 이미지를 가지고 그 위에서 처리하는 것 (edge detecting, 이미지 속에서 사물 찾기, color change)
  * 컴퓨터 그래픽스와 비쥬얼 프로세싱의 가장 큰 차이점은 **creating** (즉 컴퓨터 그래픽스는 새로운 것을 만든다는 것)

* **Modeling**
  * 컴퓨터가 이해하고 처리할 수 있는 형태로 물체를 표현한 것을 **모델(Model)**, 이러한 모델들을 만드는 과정을 **모델링**이라고 한다
  * 대부분의 3D 모델은 real time graphic에서 polygen meshes(폴리곤)로 나타난다

* **Riggint**
  * 야구선수 모델은 공을 칠 수 있어야하고, 달릴 수 있어야한다 => **Animate the plyaer**
  * 모델 안에 뼈대를 심는다
  * 3D 메쉬로 이루어진 동일한 포즈로 뼈를 심는다
  * 뼈대와 3차원 포인트들간의 상관관계(기준좌표계를 설정)를 정의
   ![image](https://user-images.githubusercontent.com/68818952/132814556-f5ba7977-6544-468a-b56e-c21c40d99410.png)

* **Animation**
  * The graphics artist create a sequence of skeletal motions
  * At run time, the skeletal motions are replayed and the polygon mesh is animated over freams
  * 실시간으로 스켈레톤 모션이 플레이 되면, 아티스트가 정해놓은 모션에 따라 폴리곤 메쉬가 같이 움직임
  * The artist perform modeling, rigging, and animation in an off-line mode

* **Rendering**
  * 3D scene에서 2D 이미지를 생성해내는 과정을 Rendering
  * 여기서 만들어진 image를 frame이라고 하기도 한다


# Applications

# Overview of 3D computer graphics production
  * Modeling, Rendering, Animation
