# Box Shadow property

Add shadows to your elements.

```css
#element {
	box-shadow: horizontal vertical blur spread color inset
}
```

## Properties

### Horizontal & Vertical

Defines where the shadow appears relative to the element.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 10px 10px black; background-color: blue; width: 100px; height: 50px;"></div></div>

### Blur

Defines how blurred the edges of the shadow are.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 10px 10px 5px black; background-color: blue; width: 100px; height: 50px;"></div></div>

### Spread

Defines the size of the shadow.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 10px 10px 5px 10px black; background-color: blue; width: 100px; height: 50px;"></div></div>

### Color

Defines the colour of the shadow.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 10px 10px 5px 10px grey; background-color: blue; width: 100px; height: 50px;"></div></div>

### Inset

Defines whether the shadow appears inside or outside the element.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 10px 10px 5px black inset; background-color: blue; width: 100px; height: 50px;"></div></div>

## Multiple shadows

You can add multiple shadows by separating each definition with a comma.

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 5px 5px 5px black, -5px 5px 5px black; background-color: blue; width: 100px; height: 50px;"></div></div>

### Paper-like shadow

<div style="background-color: white; width: 200px; height: 100px; display:flex; justify-content: center; align-items: center">
<div style="box-shadow: 0px 4px 8px 0px grey, 0px 6px 20px 0px grey; background-color: blue; width: 100px; height: 50px;"></div></div>
