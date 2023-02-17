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
위는 vertex shader 코드 일부이다. 
