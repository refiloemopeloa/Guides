## Arrow functions

Also known as lambda functions.

Allows you to create a function without explicit declaration.

Normal function:

```js
function myFunction() {
	// do stuff
}
```

Arrow function with declaration:

```js
const myFunction = () => {
	// do stuff
}
```

Arrow function without declaration:

```js
() => {
	// Do stuff
}
```

### Arguments

You can pass arguments to arrow functions just as you pass them to normal functions:

```js
(argument1, argument2) => {
	// do something with argument1 and argument2
}
```

### Immediately Invoked Function Expression

This is when you call an arrow function immediately after initializing it.

```js
() => {
	// Do stuff
}()
```

