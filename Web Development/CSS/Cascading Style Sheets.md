# Cascading Style Sheets

CSS is used to add styles to HTML.

## Basic syntax

CSS follows a basic syntax.

```css
selector {
    property: value;
}
```

## Selectors

Selectors are the HTML elements that CSS rules are applied to.

### Universal selector

Rules here will aplly to all elements

```css
* {
    color: purple;
}
```

### Type selectors

Rules will apply to all elements of the speficied selector.

```css
div {
    color: white;
}
```

### Class selectors

Rules will apply to elements with the given class.

```html
<!-- index.html -->

<div class="alert-text">Please agree to our terms of service.</div>
```

```css
/* styles.css */

.alert-text {
    color: red;
}
```

### ID Selectors

Rules will apply to elements with the given ID.

```html
<!-- index.html -->

<div id="title">My Awesome 90's Page</div>
```

```css
/* styles.css */

#title {
    background-color: red;
}
```

### The grouping selector

When rules overlap over selectors.

```css
.read {
    color: white;
    background-color: black;
    /* several unique declarations */
}

.unread {
    color: white;
    background-color: black;
    /* several unique declarations */
}
```

Group it together as follows:

```css
.read,
.unread {
    color: white;
    background-color: black;
}

.read {
    /* several unique declarations */
}

.unread {
    /* several unique declarations */
}
```

### Chaining selectors

Chain selectors to target elements with combinations of classes.

```html
<!-- index.html -->
<div>
    <div class="subsection header">Latest Posts</div>
    <p class="subsection preview">
        This is where a preview for a post might go.
    </p>
</div>
```

```css
/* style.css */
.subsection.header {
    color: red;
}
```

You can also chain a class and an ID.

```html
<!-- index.html -->
<div>
    <div class="subsection header">Latest Posts</div>
    <p class="subsection" id="preview">
        This is where a preview for a post might go.
    </p>
</div>
```

```css
/* style.css */
.subsection#preview {
    color: blue;
}
```

You cannot, however, chain more than one element selector.

### Descendant combinator

A descendant combinator will only cause elements that match the last selector to be selected if they also have an ancestor (parent, grandparent, etc.) that matches the previous selector.

```html
<!-- index.html -->

<div class="ancestor">
    <!-- A -->
    <div class="contents">
        <!-- B -->
        <div class="contents"><!-- C --></div>
    </div>
</div>

<div class="contents"><!-- D --></div>
```

```css
/* styles.css */

.ancestor .contents {
    /* some declarations */
}
```

Class B and C will be selected but not class D.

## Adding CSS to HTML

There are three ways to add CSS to HTML

### External CSS

Create a seperate file for CSS and link it to the HTML file by importing it in the `<head>` tag under the `<link>` element.

```html
<!-- index.html -->

<head>
    <link rel="stylesheet" href="styles.css" />
</head>
```

```css
/* styles.css */

div {
    color: white;
    background-color: black;
}

p {
    color: red;
}
```

### Internal CSS

Add CSS to the HTML file inside the `<style>` tag within the `<head>` tag.

```html
<head>
    <style>
        div {
            color: white;
            background-color: black;
        }

        p {
            color: red;
        }
    </style>
</head>
<body>
    ...
</body>
```

### Inline CSS

Add CSS directly to an HTML element.

```html
<body>
    <div style="color: white; background-color: black;">...</div>
</body>
```

## The Cascade

### Specificity

CSS declarations with more specificity will take precedence.

Inline CSS takes the highest precedence.

Following that, specificity will only be taken into account when an element has multiple, conflicting declarations targeting it.

<strong><em>Inline Style > ID selector > Class selector > Type selector > Universal Selector</em></strong>

Among selector types, the rule with more selectors will take precedence.

```css
/* rule 1 */
.subsection {
    color: blue;
}

/* rule 2 */
.main .list {
    color: red;
}
```

<em>rule 2 > rule 1</em>

### Inheritance

Certain CSS properties are inherited by an elements descendants, unless that descendant explicitly defines its own CSS rule. These include, but aren't limited to, `color`, `font-size`, `font-family`, etc.

### Rule order

If everything above has been considered and there are still conflicts, the last defined rule takes precedence.

```css
/* styles.css */

.alert {
    color: red;
}

.warning {
    color: yellow;
}
```

`warning` will take precedence.

## Layout

### Normal Flow

Specified by the order of your elements in HTML.

### Float

Quite old. Done to float images and text around.

### Tables

**Don't** use tables unless you are displaying tabular items.

### Position

Determine how elements render relative to each others positions.
#### Static

Stay in place

#### Relative

Move it around relative to the elements around it.

#### Absolute

Rip out the element and render it where ever.

#### Fixed

Leave an element where it is.

#### Sticky

Move relative to the users scrolling.\

### Display Property

#### Flexbox

```css
display: flex
```

Layout your elements in a one-dimensional fashion.

#### Grid

```css
display: grid
```

Can be a bit complicated, but its **very** powerful and responsive.

Properties from `display: flex` work for `display: grid` as well.

More on `grid` here: [[Display Grid]]

### Margins

Margins are like invisible boundaries around the element.

The margin property manipulates the top, right, bottom, and left properties.

```css
margin: top right bottom left 
```

# References

1. [The Odin Project CSS Foundations](https://www.theodinproject.com/paths/foundations/courses/foundations#css-foundations)
2. 