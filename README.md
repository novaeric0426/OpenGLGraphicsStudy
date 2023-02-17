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


