# Matplotlib

Matplotlib is a Python library that allows for plotting and visualisation of data.
## Importing Matplotlib

First, start by importing the following:

```python
import matplotlib.pyplot as plt
```
## Plot a 2D graph

### Create two points

```python
xpoints = np.array([0, 6])  
ypoints = np.array([0, 250])
```


### Plot points on axis

#### With line

```python
plt.plot(xpoints, ypoints)
```

#### Without line

```python
plt.plot(xpoints, ypoints, 'o')
```

#### Line with points

```python
plt.plot(xpoints, ypoints, marker = 'o')
```

### Add labels

#### Axis labels

```python
plt.xlabel("x-label")  
plt.ylabel("y-label")
```

#### Title label

```python
plt.title("title")
```

### Customize axis frequency

#### X-axis

```python
plt.xticks(np.arrange(start, end, step))
```

#### Y-axis

```python
plt.yticks(np.arrange(start, end, step))
```

### Adjust plot size

Change how big or small your plot is with:

```python
plt.figure(figsize=(width, height))
```

### Scatter Plots

Instead of using `plt.plot`, use

```python
plt.scatter(x,y)
```

### Grid Lines

Add grid lines by adding the following code before showing your graph:

```python
plt.grid()
```

#### Set grid line properties

* `color`
	* Colour of grid line
* `axis`
	* Sets which axis to show grid lines for.
* `linestyle`
	* Sets line style.
* `linewidth`
	* Sets width of line.

# References

1. [Matplotlib Pyplot](https://www.w3schools.com/python/matplotlib_pyplot.asp)
2. [Matplotlib Plotting](https://www.w3schools.com/python/matplotlib_plotting.asp)
3. [Matplotlib Markers](https://www.w3schools.com/python/matplotlib_markers.asp)
4. 