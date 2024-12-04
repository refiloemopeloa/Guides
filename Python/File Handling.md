
# File Handling

## Open file

To do anything to a file, you have to open it first:

```python
file = open(file_name, mode)
```

## Close file

Once your done with the file, close it to save system resources:

```python
file.close()
```

## Modes

There are various things you can do with a file

### Read

Open the file for reading the contents of the file without modifying them. Throws an error if the file does not exist.

```python
file = open(file_name, "r")
```

### Write

Open the file for writing, which overwrites whatever was in the file. Creates the file if it does not exist.

```python
file = open(file_name, "w")
```

Once you've open the file in write mode, you can write to the file.

```python
file.write(string)
```

### Append

Open the file for append, which writes new content at the bottom of the file. Creates the file if it does not exist.

```python
file = open(file_name, "a")
```

### Create

Creates the file. Throws an error if the file exists.

```python
file = open(file_name, "x")
```

### Handling of data in file

You can specify how data should be handled.

#### Text

```python
file = open(file_name, "rt")
```

#### Binary

```python
file = open(file_name, "rb")
```

## With operator

You can open, access, and close your file in a block of code.

```python
with open(file_name, mode) as file:
	# do stuff with file
```



# References

1. [File Handling in Python - GeeksforGeeks](https://www.geeksforgeeks.org/file-handling-python/)
2. [Python File Open](https://www.w3schools.com/python/python_file_handling.asp)
3. [Python File Write](https://www.w3schools.com/python/python_file_write.asp)