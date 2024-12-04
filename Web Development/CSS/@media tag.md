# The @media tag
The `@media` tag allows you to create different views for different contexts. It is applied to your code like a wrapper:

```css
@media {
/*your css*/
}
```

There are a lot of properties that go with @ media, but for creating views for desktop and mobile, we can focus on one property: `width`.  However, before this, let's get somethings out of the way

## Screen property

The screen property sets the CSS to only work for screens. There are different modes, such as print.  

```css
@media screen {

}
```

## Width

We'll primarily use `width` to detect different devices. 

The `width` property sets the width to be exact, which is a problem is you don't know what device you'll be using. To work around this, we can use `max-width`.

```css
@media screen and (max-width: value)
```

Here are the values of `value` that usually correspond to the different devices:
 
| max-width setting (px) | Device          |
| ---------------------- | --------------- |
| 320                    | Smartwatches    |
| 420                    | smaller devices |
| 600                    | phones          |

| min-width setting (px) | device                   |
| ---------------------- | ------------------------ |
| 600                    | Tablets and Large phones |
| 768                    | Large tablets            |
| 992                    | Laptops and desktops     |
| 1200                   | Monitors and desktops    |

# References

1. [media - CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)
2. [CSS @media Rule](https://www.w3schools.com/cssref/css3_pr_mediaquery.php)
3. [CSS Media Queries](https://www.w3schools.com/css/css3_mediaqueries.asp)


 