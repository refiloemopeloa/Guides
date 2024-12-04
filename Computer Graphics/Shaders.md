# Shaders in WebGL

Using shaders allows for finer customization of our graphics and models. 

For this guide, we'll be using **WebGL** through *JavaScript* as it is relatively easy to jump into, but the principles are similar for other languages.

Before we use shaders, we need to pass the data of our models to the shader programs.

## Model data

To pass our model data, we will use buffers. 

First, we need to initialize our model data. This includes defining vertices, indices, and colours. Once that is done, we can create our buffers.
### Create a buffer

To create a buffer, call the following function:

```js
const buffer = gl.createBuffer();
```

### Bind a buffer

Once you've created your buffer, you need to bind data to that buffer.

```js
// put the specified buffer in bind mode
gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
			// Specifies how to handle bound buffer

// bind the actual data to the specified buffer
gl.bufferData(gl.ARRAY_BUFFER, array, gl.STATIC_DRAW);
									// Specifies how drawing of buffer should be handled
```

### Transformation matrices

Now that you have stored your data in a buffer, you can manipulate it using shaders. However, you won't be able to see anything until you pass the transformation matrices.

Transformation matrices are used to position and orient the models in the 3D world.

#### Model-view matrix

The model-view matrix defines the position and orientation of the model in world space.

```js
const modelViewMatrix = mat4.create();
```

Once you've initialized the model-view matrix, you can apply transformations to it before sending it to the shader.

#### Projection matrix

The projection matrix sets up the camera's view and the projection properties.

```js
const projectionMatrix = mat4.create();
```

Once you've created the projection matrix, you need to initialize the clip view properties:

```js
const fov = Math.PI / 4;  
const aspectRatio = canvas.width / canvas.height;  
const near = 0.1;  
const far = 100;
```

Then, set the projection matrix to the view you wish to use, i.e., perspective or orthographic.

```js
mat4.perspective(projectionMatrix, fov, aspectRatio, near, far);
```

You can now pass the projection matrix to the shader.

### Passing data to shaders

To pass data to shaders, you need to use the `getLocation` functions.

#### Uniforms

To pass uniforms, first you need to bind the variable in your code to the variable in the shader:

```js
shaderProjectionMatrix = gl.getUniformLocation(shaderProgram, "uProjectionMatrix"); 
shaderModelViewMatrix = gl.getUniformLocation(shaderProgram, "uModelViewMatrix");
```

Then, you need to set the matrices as uniforms:

```js
gl.uniformMatrix4fv(  
    shaderProjectionMatrix,  
    false,  
    projectionMatrix  
);  
  
gl.uniformMatrix4fv(  
    shaderModelViewMatrix,  
    false,  
    modelViewMatrix  
);
```

#### Attributes

To pass attributes, first you need to bind the variable in your code to the variable in the shader:

```js
// here, we'll use vertexPosition as an example
const vertexPosition = gl.getAttribLocation(shaderProgram, "aVertexPosition");
```

Then, we need to put the buffer we created above in bind mode:

```js
gl.bindBuffer(gl.ARRAY_BUFFER, vertexBuffer);
```

After this, we need to set the vertex attribute pointer from the shader to the `vertexPosition` location:

```js
const numComponents = 3;  
const type = gl.FLOAT;  
const normalize = false;  
const stride = 0;  
const offset = 0; 

gl.vertexAttribPointer(  
    vertexPosition,  
    numComponents,  
    type,  
    normalize,  
    stride,  
    offset  
);
```

Lastly, we need to enable vertex attribute arrays for `vertexPosition`:

```js
gl.enableVertexAttribArray(vertexPosition);
```

### Draw

Finally, once everything above is done, you can draw your object:

```js
// bind the index buffer
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, indexBuffer);

// draw model using indices
gl.drawElements(gl.TRIANGLES, indices.length, gl.UNSIGNED_SHORT, 0);
```

## Inside a shader

Let's have a look at what shader code looks like.

### Vertex shader

Because the vertex shader is responsible for our vertex positions in clip space, the code usually looks like this:

```c
// Projection matrix
uniform mat4 uProjectionMatrix;

// Model-view matrix
uniform mat4 uModelViewMatrix;

// VertexPosition array
attribute vec4 aVertexPosition;  

// ColorPosition array
attribute vec3 aColorPosition;  

// Sending colour of each vertex to other shaders, usually fragment shader
varying lowp vec4 vColorPosition;   

void main() {       
	// Calculating vertex position in clip space
	gl_Position = uProjectionMatrix * uModelViewMatrix * aVertexPosition;   

	// Passing vertex colour to fragment shader
	vColorPosition = vec4(aColorPosition,1.0);   
}
```

### Fragment shader

Similar to the vertex shader, the fragment shader is responsible for one thing, and that is rendering the color of each fragment on screen. The code usually looks like this:

```c
// Colour of each vertex from vertex shader
varying lowp vec4 vColorPosition;

void main() {
	// Setting colour of each fragment
	gl_FragColor = vColorPosition;    
}
```

## Steps for using shaders in WebGL

1. Create arrays for model data
2. Initialize buffers
	1. Create buffer
	2. Bind buffer
	3. Bind data
3. Create shader program
4. Bind shader variables to variables in program
5. Create transformation matrices
	1. Create model-view matrix
	2. Create projection matrix
		1. Define view mode attributes
		2. Attach view mode attributes to projection matrix
6. Set shader pointers to arrays in program
	1. Bind buffer
	2. set attribute pointer to location of array
	3. enable attribute array for given array
7. Use shader program
8. Set transformation matrices to uniform matrices
9. Bind buffer to index buffer
10. Draw elements

## Lambert Shading

Calculates lighting per-vertex and interpolates colour at every pixel.

The first thing you need to do is initialize the following variables:

```js  
let a_coords_loc;       // Location of the a_coords attribute variable in the shader program.  
let a_normal_loc;       // Location of a_normal attribute.  
  
// Locations of uniform variables in the shader program  
let u_diffuseColor;     // diffuse color  
let u_specularColor;    // specular color  
let u_specularExponent;     // specular exponent  
let u_lightPosition;    // light position  
  
let u_modelview;    // modelview matrix  
let u_projection;   // projection matrix  
let u_normalMatrix;    // normal matrix
```

Then you need to initialize them in your vertex shader:

```c
const lambertVertexShaderSource = `  
    // Vertex shader for a lambert lighting model.  


    // attributes  

	// a_coords: 3D coordinates of the vertex.    
    attribute vec3 a_coords;  

	// a_normal: Normal vector at the vertex.    
    attribute vec3 a_normal;  


    // uniforms  
    
    // modelview: Modelview matrix.    
    uniform mat4 modelView;  
    
    // projection: Projection matrix.    
    uniform mat4 projection;  
    
    // normalMatrix: Normal matrix.    
    uniform mat3 normalMatrix;  
    
    // diffuseColor: Diffuse color.    
    uniform vec4 diffuseColor;  
    
    // specularColor: Specular color.    
    uniform vec3 specularColor;  
    
    // specularExponent: Specular exponent.    
    uniform float specularExponent;  
    
    // lightPosition: Position of the light source.    
    uniform vec4 lightPosition;  
```

Now, bind the program variables with the shader variables:

```js
a_coords_loc =  gl.getAttribLocation(lambert_prog, "a_coords");  
a_normal_loc =  gl.getAttribLocation(lambert_prog, "a_normal"); 

u_modelview = gl.getUniformLocation(lambert_prog, "modelview");  
u_projection = gl.getUniformLocation(lambert_prog, "projection");  
u_normalMatrix =  gl.getUniformLocation(lambert_prog, "normalMatrix");  

u_diffuseColor =  gl.getUniformLocation(lambert_prog, "diffuseColor");  
u_specularColor =  gl.getUniformLocation(lambert_prog, "specularColor");  
u_specularExponent =  gl.getUniformLocation(lambert_prog, "specularExponent");  
u_lightPosition =  gl.getUniformLocation(lambert_prog, "lightPosition");
```

Then, add the following variables:

```c
// Vectors  
  
// eyeCoords: Coordinates of the vertex in eye coordinates.  
vec3 v_eyeCoords;  
  
// normal: Normal vector at the vertex.  
vec3 v_normal;  
  
// Fragment shader variables  
varying vec4 fragment_color;
```

Now, lets look at the actual code for our vertex shader:

```c
void main() {

// 1. compute the eye coordinates of the vertex.
	vec4 coords = vec4(a_coords, 1.0);
	vec4 eyeCoords = modelView * coords;
	gl_Position = projection * eyeCoords;

// 2. compute the normal vector at the vector
	v_normal = normalize(a_normal);

// 3. compute the eye coordinates of the vertex
	v_eyeCoords = eyeCoords.xyz/eyeCoords.w;

// 4. compute lighting equation

	// 4.1. Declare vectors for lighting equation
	vec3 N, L, R, V;

	// 4.2. Compute N
	N = normalize(normalMatrix * v_normal);

	// 4.3. Compute L
	if (lightPosition.w == 0.0) {
		L = normalize(lightPosition.xyz);
	} else {
		L = normalize(lightPosition.xyz/lightPosition.w - v_eyeCoords);
	}

	// 4.3. Compute R
	R = -reflect(L,N);

	// 4.4. Compute V
	V = normalize(-v_eyeCoords);

// 5. Compute fragment colour
	if (dot(L,N) <= 0.0) {
		fragment_color = vec4(0,0,0,1);
	} else {
		vec3 color = 0.8*dot(L,N) * diffuseColor.rgb;
		if (dot(R,V)>0.0) {
			color += 0.4 * pow(dot(R,V), specularExponent) * specularColor;
		}
		fragment_color = vec4(color, diffuseColor.a);
	}
}
```

Finally, pass the `fragment_color` to the fragment shader:

```c
varying vec4 fragment_color;

void main() {
	gl_FragColor = fragment_color;
}
```

### Steps for Lambert Shading

1. Declare variables.
	1. Attributes.
		1. Model Coordinates.
		2. Normal Matrix.
	2. Uniforms.
		1. Vectors
			1. Diffuse color.
			2. Specular color.
			4. Light position.
		2. Scalars
			1. Specular exponent.
		3. Matrices
			1. Model-view.
			2. Projection.
			3. Normal.
	3. Program variables.
		1. Projection matrix.
		2. Model-view matrix.
		3. Normal matrix.
2. Get locations of variables and pass to shader.
	1. Attributes.
	2. Uniforms.
3. Initialize variable values.
	1. Attributes.
		1. Attribute pointers.
	2. Uniforms.
		1. Uniform functions.
4. Vertex Shader.
	1. Declare attributes and uniforms passed from program.
	2. Declare:
		1. Eye coordinates.
		2. Normal vector.
		3. Fragment color.
	3. Compute `gl_Position`.
	4. Compute normal vector.
	5. Compute eye coordinates.
	6. Compute lighting equation.
		1. Compute N.
		2. Compute L.
		3. Compute R.
		4. Compute V.
	7. Compute fragment color.
5. Fragment Shader.
	1. Receive fragment color vector.
	2. Set `gl_FragColor`.

## Phong shading

Similar to Lambert, but lighting equation is done in fragment shader.

### Vertex shader

Get model-view and projection matrix.
Calculate eye coordinates.
Calculate coordinate of vertex.
Calculate `gl_Positon`

Calculate and pass normal vector.
Calculate and pass eye coordinates.

### Fragment shader

Accept normal vector and eye coordinates.
Get diffuse color, specular color, specular exponent, light position and normal matrix.
Declare N, L, R, V.
Compute N by normalizing product of normal matrix and normal vector.
Compute L by first checking light position fourth coordinate is greater than zero, then set L equal to: `normalize(light_position.xyz/light_position.w) - v_eyeCoords`.  
Compute R by setting R to `-reflect(L,N)`.
Compute V by setting V to `normalize(-v_eyeCoords)`

Compute diffuse component.
Compute specular component.

Set gl_FragColor.