# display : grid

`display : grid` is a powerful and responsive display view. It involves a lot of preplanning, but it allows you to really fine tune how things are laid out on the screen.

## Structure

The basic `grid` set up should have the following:

```css
display : grid;

grid-template-columns : attribute attribute attribute ...

grid-template-row : attribute attribute attribute ...

grid-column: value value ...

grid-row: value value ...
```

## grid-template

These set the column and row sizes.

### track-size

Determines the space allocations in the grid. Can be in length, percentage, or a fraction (`fr`).

### line-name 

Arbitrary name of a line. You choose it.

### Example

```css
.container { 
	grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end]; 
	grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line]; 
}
```

This results in:

<img src="https://css-tricks.com/wp-content/uploads/2018/11/template-columns-rows-01.svg" width=400px style="background-color: white"/>

### Note

Lines can have more than one name by including more than one in the square brackets, seperated by spaces:

```css
[line1-end line2-start]
```

You can also streamline line creation with the `repeat` function:

```css
.container { 
	grid-template-columns: repeat(3, 20px [col-start]); 
}
```

which equates to:

```css
.container {
	grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start]; 
}
```

If multiple lines share the same name, they can be referenced by their line name and count:

```css
.item { 
	grid-column-start: col-start 2; 
}
```

### grid-template-areas

Define your grid area by naming grid sections with the `grid-area` property and sectioning your grid with these names.

#### grid-area

Name a grid area here. A grid area is equal to one grid division, which is determined by the row sizes and column sizes.

```css
.item-a {
	grid-area: header; 
} 
.item-b { 
	grid-area: main; 
} 
.item-c { 
	grid-area: sidebar; 
} 
.item-d { 
	grid-area: footer; 
}
```

A dot, `.` signifies an empty cell.
`none` means a grid area was not defined.

```css
.container { 
grid-template-areas: "<grid-area-name> | . | none | ..." 
					 "..."; 
}
```
#### Example

```css
.item-a { 
	grid-area: header; 
} 
.item-b { 
	grid-area: main; 
} 
.item-c { 
	grid-area: sidebar; 
} 
.item-d { 
	grid-area: footer; 
} 
	.container { 
	display: grid; 
	grid-template-columns: 50px 50px 50px 50px; 
	grid-template-rows: auto; 
	grid-template-areas: "header header header header" 
	"main main . sidebar" 
	"footer footer footer footer"; 
}
```

This results in:

<img src="https://css-tricks.com/wp-content/uploads/2018/11/dddgrid-template-areas.svg" width=400px style="background-color: white"/>

#### Note

Pay attention to how rows and columns are differentiated. Every thing in one row is in the same string, separated by spaces. These all form columns. Different rows are different strings seperated by closed and open quotation marks.

```css
row1: "[0][0] [0][1] [0][2]"
row2: "[1][0] [1][1] [1][2]"
```

When using `grid-area`, lines are automatically named for you with the following syntax:
```css
your_grid-start
your_grid-end
```


### fr

The `fr` unit allows you to set fractional values which are automatically calculated for you based on the free space available:

```css
.container { 
	grid-template-columns: 1fr 1fr 1fr; 
}
```

This will divide the columns into thirds. Note that free space is calculated after any items are rendered.

### repeat

`repeat` allows you to generate grid constraints on the fly.

```css
repeat(num_of_repeats, constraint_to_be_repeated)
```

#### num_of_repeats

`num_of_repeats` can take any of the following values:

##### auto-repeat

Determine how many repeats based on the constraint.

* `auto-fit`
	* fits the currently available columns into the space by expanding the columns, so that the take up the available space.
* `auto-fill`
	* fills the row with as many columns as can fit.
	* creates columns whenever a new column can fit.

Here's an example:


auto-fill

<body style="padding: 2em;">
<div style="display: grid;
grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
			background-color: white
	 ">
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    1
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    2
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    3
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    4
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    5
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    6
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    7
  </div>
</div>
</body>

<hr>

auto-fit
<body style="padding: 2em;">
<div style="display: grid;
grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
			background-color: white
	 ">
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    1
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    2
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    3
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    4
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    5
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    6
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    7
  </div>
</div>
</body>

At a small enough size, it seems like `auto-fit` and `auto-fill` do the same thing. But observe what happens when i increase the available space:

auto-fill

<body style="padding: 2em;">
<div style="display: grid;
grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
			background-color: white
	 ">
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    1
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    2
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    3
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    4
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    5
  </div>
</div>
</body>

<hr>

auto-fit
<body style="padding: 2em;">
<div style="display: grid;
grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
			background-color: white
	 ">
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    1
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    2
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    3
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    4
  </div>
  <div style="
background-color: deepPink;
  padding: 20px;
  color: #fff;
  border: 1px solid #fff;
">
    5
  </div>
</div>
</body>

Notice that `auto-fit` fills up the available space, whereas `auto-fill` stays true to the column size.

`auto-repeat` only works with `fixed-size`.
##### fixed-repeat

Set the number of repeats.

Only works with `fixed-size`.

##### track-repeat

Set the number of repeats.

Only works with `track-size`.

#### constraints_to_be_repeated

`constraints_to_be_repeated` can be any of the following:

* `fixed-size`
	* a `length-percentage` value
* a `minmax` function with:
    - `min` given as a `length-percentage` value
	- `max` given as one of a `length-percentage` value, a `flex` (`fr`) value, or one of the following keywords: `min-content`, `max-content`, or `auto`.
* a `minmax` function with:
    - `max` given as a `length-percentage` value
	- `min` given as one of a `length-percentage` value, a `flex` (`fr`) value, or one of the following keywords: `min-content`, `max-content`, or `auto`.

Here's an example:

<div
	 style="
  display: grid;
  grid-template-columns: repeat(2, 50px 1fr) 100px;
  grid-gap: 5px;
  box-sizing: border-box;
  height: 200px;
  width: 100%;
  background-color: #8cffa0;
  padding: 10px;
">
  <div style="
  background-color: #8ca0ff;
  padding: 5px;
"
  >This item is 50 pixels wide.</div>
  <div style="
  background-color: #8ca0ff;
  padding: 5px;
"
  >Item with flexible width.</div>
  <div style="
  background-color: #8ca0ff;
  padding: 5px;
"
  >This item is 50 pixels wide.</div>
  <div style="
  background-color: #8ca0ff;
  padding: 5px;
"
  >Item with flexible width.</div>
  <div style="
  background-color: #8ca0ff;
  padding: 5px;
"
  >Inflexible item of 100 pixels width.</div>
</div>

# References
 1. [CSS Grid Layout Guide | CSS-Tricks](https://css-tricks.com/snippets/css/complete-guide-grid/)
 2. [CSS Grid Layout (w3schools.com)](https://www.w3schools.com/CSS/css_grid.asp)
 3. 