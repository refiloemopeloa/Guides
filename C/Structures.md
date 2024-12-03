# Structures in C

Structures are an encapsulation of variables. Each variable in a structure is known as a **member** of the structure. Structures are very similar, if not identical to `dictionaries` in Python, or `objects` in JavaScript.

## Create a structure

You create a structure using the `struct` keyword, followed by the name of that structure. Any members are declared inside curly brackets:

```C
struct struct_name {
	data_type member1;
	data_type member2;
	...
	...
};
```

## Using a structure

To use a structure, you need to declare an instance of that structure:

```C
int main() {
	struct struct_name a, b, c;
	return 0;
}
```

You can also declare the instances with the structure creation:

```C
struct struct_name {
	data_type member1;
	data_type member2;
	...
	...
}a, b, c;
```

## Initialize structure members

You can initialize a structure in one of three ways:

### 1. Assignment operator

```C
struct struct_name a;  
a.member1 = value1;  
a.member2 = value2;  
```

### 2. Initializer List

```C
struct structure_name a = { value1, value2 };
```

#### Note

In this type of initialization, the values are assigned in sequential order as they are declared in the structure template.

### 3. Designated Initializer List

```C
struct structure_name a = { .member1 = value1, .member2 = value2 };
```

#### Note

This type of initialization allows us to initialize in any order. It is only available from the *C99 standard* and only supported in C, not C++.

## Accessing structure members

To access members of a structure, use the dot syntax (`.`):

```C
int main() {
	struct struct_name a;

	a.member_name1 = 5;
	a.member_name2 = 'c';
	
	return 0;	
}
```

### Setting member values on instantiation

You can assign values to members upon instantiating a struct instance using `{}`:

```C
int main() {
	struct my_struct a = {5, 'c'};
	return 0;
}
```

### Modifying member values

Since members are just variables, they can be modified the same way you would modify a single-standing variable.

## Copying structures

Since structures are treated as a datatype, equating two structures copies the data of the first structure to the new structure.

```C
int main() {
	struct myStructure s1 = {13, 'B', "Some text"};  
	struct myStructure s2;  
	  
	s2 = s1;
}
```

## typedef for structures

Initiating structures can be tedious because of how much code is needed. We can shorten this by using `typedef`:

```C
typedef struct {
	int a;
	int b;
} my_struct

int main() {
	my_struct one = { 0 };  // initializes both .a and .b to 0;
}
```

## Nested structures

Structures can be nested as follows:

### 1. Embedded Structure Nesting

```C
struct parent {  
    int member1;  
    struct member_str member2 {  
        int member_str1;  
        char member_str2;  
        ...  
    }  
    ...  
}
```

### 2. Separate Structure Nesting

```C
struct member_str {  
    int member_str1;  
    char member_str2;  
    ...  
}  
  
struct parent {  
    int member1;  
    struct member_str member2;  
    ...  
}
```

## Self-Referential Structures

A self-referential structure is a structure that contains reference(s) to the same type as itself:

```C
struct structure_name {  
    data_type member1;  
    data_type member2;  
    struct structure_name* str;  
}
```

## C Structure Padding and Packing

Intuitively, you would assume the size of a struct is the sum of the sizes of its members. But you'll find that this isn't the case. 

Let's take a look at an example below:

```C
#include <stdio.h>

struct a {
	int i;  //4 bytes
	char c;  //1 byte
};

int main() {
	printf("Size of struct a: %ld bytes", sizeof(struct a));
}
```

You would expect the output to be 5 bytes, but when you run the above program, you'll find that the output is actually:

```shell
Size of struct a: 8 bytes
```

The reason for the is **Structure Padding**

### Structure padding

**Structure padding** is the concept of adding one or more empty bytes in a structure to naturally align the data members in the memory. It is done to minimize the CPU read cycles to retrieve different data members in the structure.

To understand what this means, let us first talk about how the processor reads data. The processor does not read 1 byte at a time. It reads 1 word at a time. What is a word you ask? Well, it depends on your processor. To get how big a word is for your processor, simply divide the bit rating by 8.
* 32-bit = 4 bytes per word
* 64-bit = 8 bytes per word

How does this minimize CPU read cycles? Well, suppose we're working with a 32-bit processor and we had the following dictionary:

```C
struct student  
{  
	char a; // 1 byte  
	char b; // 1 byte  
	int c; // 4 bytes   
}
```

Let's take a look at it in memory without padding:

<img src="https://d2jdgazzki9vjm.cloudfront.net/cpages/images/structure-padding-in-c1.png">

If we wanted to access `a` and `b`, then we can do that in one read, no doubt. But what if we wanted to access `c`? This would need to be done in two reads. Once we add padding:

<img src="https://d2jdgazzki9vjm.cloudfront.net/cpages/images/structure-padding-in-c2.png">

Now, if we want to access just `c`, we can do this in just one read.

Structure padding basically allows us to read data in the minimum required reads.

But, what if we want our data tightly packed? What if we have memory limitations? What if we want to use exactly the amount of memory the struct should take?


### Structure packing

**Structure packing** involves explicitly telling the compiler not to add padding, but to keep struct to exact size of sum of members. C language provides two ways for structure packing:

1. Using `#pragma pack(1)`

	```C
	#pragma pack(1)  
	struct a {  
		int i;  
		char c;  
	} ;
	```

2. Using `__attribute((packed))__`

	```C
	struct a {  
	    int i;  
	    char c;  
	} __attribute((packed)) __;
	```

Now if we take a look at our output:

```shell
Size of struct a: 5 bytes
```

## Bit Fields

Bit Fields are used to specify the length of the structure members in bits. When we know the maximum length of the member, we can use bit fields to specify the size and reduce memory consumption:

```C
struct structure_name {  
    data_type member_name: width_of_bit-field;  
};
```


# References

1. [C Structures (structs) (w3schools.com)](https://www.w3schools.com/c/c_structs.php)
2. [C Structures - GeeksforGeeks](https://www.geeksforgeeks.org/structures-c/)
3. [Structure Padding in C - javatpoint](https://www.javatpoint.com/structure-padding-in-c)