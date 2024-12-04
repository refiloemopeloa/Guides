# File Handling in JavaScript

## Read a file

This can be done using the `fetch` API:

```js
fetch('file_name').then(response => response.text()).then(data => {
// Do something with your data
})
```