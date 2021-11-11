## WebGL: Scene Data
![image](https://user-images.githubusercontent.com/68818952/141311639-26a500f1-bafe-48fc-9d93-855b191bdac2.png)
* 점을 찍을 때 점의 사이즈를 미리 정해줄 수 있다.
* **gl.TRIANGLES**를 주로 많이 사용할 것 이다.
* vertex position, normal, column들을 그릴 때 primitive type
* position array와 color array의 length가 같아야 한다.
* 자바스크립트에서는 array로 표현한다.
![image](https://user-images.githubusercontent.com/68818952/141312084-52cc0593-fdff-4add-ac56-c604baae7c84.png)

## WebGL: Passing scene data to vertex shader
1. Create a buffer object(gl.createBuffer())
2. Bind the buffer object to a target(gl.bindBuffer())
3. Write data inro the buffer object(gl.bufferData())
4. Assgin the buffer object to an attribute variable(gl.vertexAttributePointer())
5. Enable assignment(gl.enableVertexAttribArray())
* position array와 color array 동일한 방법으로 만든다.

## WebGL Program - Initialize shaders
1. Create shader object(gl.createShader())
2. Store the shader programs(gl.shaderSource())
3. Compile the shader objects(gl.compileShader())
4. Create a program object(gl.createProgram())
5. Attach the shader objects to the program object(gl.attachShader())
6. Link the program object(gl.linkProgram())
7. Tell the WebGL system the program object to be used(gl.useProgram())
