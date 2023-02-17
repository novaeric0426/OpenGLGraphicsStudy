# OpenGL로 피라미드 만들어보기(with image texture)

## 선행으로 알아야 할 수학적 개념

### 1.아핀 변환

```
uniform mat4 model;
uniform mat4 projection;
uniform mat4 view;

void main()
{
	gl_Position = projection * view * model * vec4(pos, 1.0);
	vCol = vec4(clamp(pos, 0.0f, 1.0f), 1.0f);
	
	TexCoord = tex;
}
```
위는 vertex shader 코드 일부이다. 3차원은 (x,y,z)로 이루어졌지만 연산 과정은 4x4 matrix를 이용해서 계산된다. 이는 좌표의 위치변환을 행렬의 곱셈으로 표현하기 위하여 1차원을 더 추가하여 사용한다.(homogeneous coordinate)

### 2. Coordinate System

![image](https://user-images.githubusercontent.com/56947207/219658341-dac4b26f-27f8-4f65-ac3a-8313df8adbc5.png)

행렬식의 연산순서에 의해 model, view, projection 행렬 순으로 vertex 좌표에 곱해진다. 
- model : 화면에 보여지는 오브젝트는 (0,0,0)을 중심으로 하는 local space에서 정의. 이를 world space 좌표로 변환.
- view : world에 존재하는 camera의 시점으로 보는 view space 좌표로 변환
- projection : clip 좌표로 투영하여 화면에 vertex들이 그려질것인지 아닌지를 판단. OpenGL은 view 좌표를 clip 좌표로 변환할 때 2개의 방식을 사용(orthographic, perspective)

### 3. Camera 구현

![image](https://user-images.githubusercontent.com/56947207/219706867-8cea5ae3-7dc2-4c41-9c1c-3c5bf5d654cd.png)

![image](https://user-images.githubusercontent.com/56947207/219707035-e0bfc758-de30-490f-873f-01e3c02a66e5.png)

R : right vector

U : up vector

D : direction vector

P : camera의 position vector

![image](https://user-images.githubusercontent.com/56947207/219707540-d9d2e994-87af-4743-bcee-1ae534b5dd6f.png) ![image](https://user-images.githubusercontent.com/56947207/219707591-932c220c-2f06-4198-823c-c0babb01b602.png)

```
void Camera::update()
{
	front.x = cos(glm::radians(yaw)) * cos(glm::radians(pitch));
	front.y = sin(glm::radians(pitch));
	front.z = sin(glm::radians(yaw)) * cos(glm::radians(pitch));
	front = glm::normalize(front);

	right = glm::normalize(glm::cross(front, worldUp));
	up = glm::normalize(glm::cross(right, front));
}
```



