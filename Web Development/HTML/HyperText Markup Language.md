# HyperText Markup Language

HTML defines the structure and content of webpages

## Semantic HTML

Designing webpages with a wider range of accessibility. Examples of this are users who access the web through screen readers.

## Elements & Tags

### Elements

Pieces of content

#### Examples of elements

-   header
-   body
-   footer
-   heading
-   section
-   div
-   spanner
-   anchor
-   table
-   unordered list
-   icon

### Tags

Wrappers around pieces of content

#### Examples of tags

```html
<header></header>
<body></body>
<footer></footer>
<h1></h1>
<section></section>
<div></div>
<span></span>
<a></a>
<table></table>
<ul></ul>
<i></i>
```

### Void Elements

Some elements do not have closing tags

#### Examples of void elements

-   image

```html
<img />
```

-   line break

```html
<br />
```

## Boilerplate

Basic structure that all HTML documents have and need to be in place before anything useful is done.

### DOCTYPE

Tells the browser which version of HTML to use to render

```html
<!DOCTYPE html>
```

### HTML element

Root element of document. Wraps around every other element.

```html
<html></html>
```

### Head element

Important meta-info about our webpages, and required stuff for correct rendering of our webpages in the browser. Not for displaying content.

#### Meta element

Set the encoding of the webpage with the `charset` attribute (more on attributes later in this document).

```html
<meta charset="utf-8" />
```

#### Title element

Gives webpage a human-readable title, displayed in the webpage's browser tab.

```html
<title>Text Here</title>
```

### Body element

Content that is displayed to users is wrapped by the body

```html
<body></body>
```

### VSCode shortcut

If you are using VSCode, you can populate your HTML document with basic boilerplate by typing the exclamation mark `!` on your keyboard and pressing the <kbd>Enter</kbd> key.

## Text

### Paragraphs

For bodies of text

```html
<p>Paragraph here</p>
```

Output:

<p>Paragraph here</p>

### Headings

For headings. Range from `<h1>` to `<h6>`.

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```

Output:

<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>

### Font style through elements

#### Strong element

The `<strong>` element makes text bold and marks it as important sematically.

```html
<p><strong>Text Here</strong></p>
```

Output:

<p><strong>Text Here</strong></p>

##### Em element

The `<em>` element makes text italic and places emphasis on it semantically.

```html
<p><em>Text Here</em></p>
```

Output:

<p><em>Text Here</em></p>

##### HTML Comments

Comments are not visible to the browser and are primarily for the developer and pther developers.

```html
<!-- HTML Comment -->
```

## Lists

Every list has list item elements, `<li>`

### Unordered Lists

A list where order doesn't matter.

```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

Output:

<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

### Ordered Lists

A list where order matters

```html
<ol>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ol>
```

Output:

<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ol>

## Links and Images

### Anchors

Anchors are how we make links in HTML.

```html
<a href="https://www.theodinproject.com/about">About The Odin Project</a>
```

Output:

<a href="https://www.theodinproject.com/about">About The Odin Project</a>

`href` is an attribute which is where you are directed to when you click the link. Without `href`, an anchor looks like plain text.

The `target` attribute allows you to do things like open the page in a new tab with `_blank` or the current page with `_self`.

The `rel` attribute allows you to manage the relation between the current page and the linked document. The `noopener` value prevents the opened link from gaining access to the webpage from which it was opened and the `noreferrer` value prevents the opened link from knowing which webpage or resource has a link (or ‘reference’) to it. If you are curious why this is necessary, this article about [tabnabbing](https://owasp.org/www-community/attacks/Reverse_Tabnabbing) is a great resource.

#### Absolute links

Links to pages on other websites on the internet. Made up of the following template: `protocol://domain/path`

```html
<a href="https://www.theodinproject.com/about">About Thw Odin Project</a>
```

#### Relative links

Links to pages within our website. Made up of the following template:
`directory/page`

```html
<a href="about.html">About</a>
```

### Images

Display an image in HTML.

```html
<img src="https://www.theodinproject.com/mstile-310x310.png" />
```

Output:
<img src="https://www.theodinproject.com/mstile-310x310.png">

#### Alt attribute

Alternative text for the image. Used to describe the image.

```html
<img
    src="https://www.theodinproject.com/mstile-310x310.png"
    alt="The Odin Project Logo"
/>
```

#### Image size attributes

You can specify the image `width` and `height` if you don't want to use th edefault image size.

```html
<img
    src="https://www.theodinproject.com/mstile-310x310.png"
    alt="The Odin Project Logo"
    height="310"
    width="310"
/>
```

Output:
<img src="https://www.theodinproject.com/mstile-310x310.png" alt="The Odin Project Logo" height="310" width="310">

##

# References

1. [HTML Foundations | The Odin Project](https://www.theodinproject.com/paths/foundations/courses/foundations#html-foundations)
2. 