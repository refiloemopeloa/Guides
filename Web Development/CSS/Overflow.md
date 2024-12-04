# Overflow

Overflow allows content to flow past the display width.

## Scroll on mobile

If you want to create a navigation system with options that exist beyond what can fit on screen, you can add the following to your code:

```css
    .categories-row {
        display: grid;
        grid-auto-flow: column;
        grid-auto-columns: 100px;
        overflow-x: auto;
        overscroll-behavior-x: contain;
        scroll-snap-type: x mandatory;
        scrollbar-width: none; /* For Firefox */
        -ms-overflow-style: none; /* For Internet Explorer and Edge */
    }
```

# References

1. [Make a scrollable row that doesn't wrap using display grid](https://claude.ai/)
2. 