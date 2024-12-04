# Time in Python

The `time` library in python allows you to do time related processing and tasks.

First, import the library:

```python
import time
```

## Get current time

To get the current time in seconds since epoch, use the following function:

```python
current_time = time.time()
```

The return value is a float, which means you convert to smaller time steps by dividing by $10^{3k},\ where\ k \in \mathbb{Z},$ as many times as you need.
