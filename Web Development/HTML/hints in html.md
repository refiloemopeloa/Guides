# HTML Hints
Hints in HTML involve a bit of initialization before we can use them.

## Hint element

### HTML

The first thing you'll need to do is create a storage container for the hint. For this example, we'll be using a `div`:

```html
<div id="hint"></div>
```

Then, create a span in the `div`:

```html
<div id="hint">
	<span id="hint-text">
		Hint text here
	</span>
</div>
```

Once this is done, surround whatever you'd like your hint to appear over. In this example, we'll be giving a button a hint:

```html
<div id="hint">
	<button>
		Click Me!
	</button>
	<span id="hint-text">
		Hint text here
	</span>
</div>
```

### CSS

Now for the CSS. It is up to you if you would like to do inline CSS or external CSS. For this example, I'll be using internal CSS. Add the following to your stylesheet:

```css
#hint {  
	position: relative;  
	display: inline-block;  
}  
  
/* hint text */  
#hint #hint-text {  
	visibility: hidden;  
	width: 120px;  
	background-color: black;  
	color: #fff;  
	text-align: center;  
	padding: 5px 0;  
	border-radius: 6px;  
   
  /* Position the hint text - see below for different positions */  
  position: absolute;  
  z-index: 1;
}  
  
/* Show the tooltip text when you mouse over the tooltip container */  
#hint:hover #hint-text {  
	visibility: visible;
}
```

## Hint Attributes
### Position

You can customize where you'd like the hint to appear by adding this to the `#hint #hint-text` section:
#### Right Tooltip

```css
top: -5px;  
left: 105%;
```
#### Left Tooltip

```css
top: -5px;  
right: 105%;
```

#### Bottom Tooltip

```css
  width: 120px;  
  top: 100%;  
  left: 50%;  
  margin-left: -60px; /* Use half of the width (120/2 = 60), to center the tooltip */
```
#### Top Tooltip

```css
  width: 120px;  
  bottom: 100%;  
  left: 50%;  
  margin-left: -60px; /* Use half of the width (120/2 = 60), to center the tooltip */
```

### Arrows

You can also add arrows from the hint to the element:

#### Bottom Arrow

```css
#hint #hint-text::after {  
	content: " ";  
	position: absolute;  
    top: 100%; /* At the bottom of the tooltip */  
    left: 50%;  
	margin-left: -5px;  
	border-width: 5px;  
	border-style: solid;  
	border-color: black transparent transparent transparent;
}
```

#### Top arrow

Change the `top` attribute to `bottom`.

#### Left arrow

Change the `left` to `right` and change its value from `50%` to `100%`. Also, change `top` from `100%` to `50%`.

#### Right arrow

Change the `left` value from `50%` to `100%`. Also, change `top` from `100%` to `50%`.

### Fade In Animation

You can add an extra bit of flare by adding an animation to the hint:

```css
#hint #hint-text {  
	opacity: 0;  
	transition: opacity 1s;
}  
  
#hint:hover #hint-text {  
	opacity: 1;
}
```

## Hints in React

Implementing a hint in react is fairly simple as its just slightly changing the above code.

Create a file called `hint.js` and in it, add the following code:

```js
import "./hint.css"

export function Hint({hintText, children}) {  
    return (  
        <div id="hint">  
            {children}  
            <span id="hint-text">  
                {hintText}  
            </span>  
        </div>  
    );}
```

Create a file called `hint.css` and copy the CSS we implemented earlier in the HTML example.

Then, import the hint object in the file you are working in, and add it to the returned renders:

```js
export function SomePage() {
	return(
	<>
		<Hint hintText="Your hint">
			//add elements that you want to be affected by the hint here
		</Hint>
	</>
	);
}
```


## Remarks

Congratulations! You've added hints to your program and made it more user-friendly!