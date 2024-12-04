# Surface Normals

## Triangles

To find the surface normal of a triangle, you need the coordinates of its vertices.

```python
v1 = np.array([0,0,0])
v2 = np.array([1,0,0])
v3 = np.array([0,1,0])
```

Next, we need to calculate two edges of the triangle.

```python
edge1 = v2 - v1
edge2 = v2 - v1
```

Once that is done, calculate the cross product of the two edges.

```python
normal = np.cross(edge1, edge2)
```

Lastly, normalize the vector.

```python
normal_length = np.linalg.norm(normal)

if normal_length == 0:
	raise ValueError("The triangle vertices are collinear (form a line)")

normalized_normal = normal / normal_length
```