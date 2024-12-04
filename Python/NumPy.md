
## Using NumPy

Import `numpy` using:

```python
import numpy as np
```

## Create an array

### One-dimensional

```python
array = np.array([])
```

### Two-dimensional

```python
array = np.array([[]])
```

#### Order of access

Row then column

```python
array[2][5]    # row 2, column 5
```

## Populate array

### Combine two one-dimensional lists into one two-dimensional list

```python
np.column_stack(([1,2,3],[4,5,6]))

# Output
[[1,4],
 [2,5],
 [3,6]]
```

### Initialize empty array

```python
np.empty(shape, dtype, order)
```

* `shape`
	* Shape of empty array.
* `dtype`
	* Output data-type for array.
* `order`
	* Whether data in multi-dimensional arrays should be stored in row-major (`C`) or column-major (`F`) order in memory.

## Accessing data in array

### 2D array

#### Accessing entire column

```python
array[:, n]    # n is column
```

#### Accessing entire row

```python
array[n, :]    # n is row
```

## Slicing arrays

Slicing is when we take elements in an array from a given index to another given index.
### 1D array

```python
array[start:end:step]
```

* `start`
	* From and including `start`.
	* If nothing is passed, `start` is `0`.
* `end`
	* Up to and excluding `end`.
	* If nothing is passed, `end` is `len(array)`.
* `step`
	* Step value through array.
	* If nothing is passed, `step` is `1`.
### Negative slicing

Used to refer to an index from the end.

`array[-3:-1] => array[end-3:end-1]`

### 2D array

```python
array[start:end:step, start:end:step]
```

## Appending to array

`np.append` returns a new array which is the old array with the new items appended.

```python
np.append(array, values, axis)
```

* `array`
	* Old array which values are appended to.
* `values`
	* Values that are appended to the old array.
* `axis`
	* Axis along which values are appended.
	* Default value is `None`.
	* If no value is passed, array is flattened before returning.

Here's an example:

```python
array = np.array([[1,2,3,4]])

# No axis
array = np.append(array, [5,6,7,8])
# Output:
# [1,2,3,4,5,6,7,8]

# Axis = 0
array = np.append(array, [5,6,7,8], axis = 0)
# Output:
# [[1,2,3,4],
#  [5,6,7,8]]

# Axis = 1
array = np.append(array, [5,6,7,8], axis = 1)
# Output:
# [[1,2,3,4,5,6,7,8]]
# Notice the difference between no axis - the values are added to the row that they correspond to, as opposed to flattening the array.
```

# References

1. [NumPy Array Slicing](https://www.w3schools.com/python/numpy/numpy_array_slicing.asp)
2. [numpy.append() in Python - GeeksforGeeks](https://www.geeksforgeeks.org/numpy-append-python/)
3. 