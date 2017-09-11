# Stack manipulations with ES6 destructuring

Although the HP calculator documentation often makes reference to a 'stack',
in our calculator code it is convenient to represent the 'stack' as a fixed length array
of four numbers. We don't use `push()` on this
array but instead use ES6 destructuring to decompose the 'stack' into individual `x`, `y`,
`z` and `t` values, and reconstruct a new stack from these values, using
transformations as required. This approach maps closely to our mental model of the RPN calculator stack. The code below illustrates the concept.

```js
// initial stack state
// stack: [0, 0, 0, 0]

// roll down
const [x, y, z, t] = state.stack
const stack = [t, x, y, z]

// swap x and y
const [x, y, ...rest] = state.stack
const stack = [y, x, ...rest]

// apply a function to x
const [x, ...rest] = state.stack
const stack = [fn(x), ...rest]

// apply a function to x and y
const [x, y, z, t] = state.stack
const stack = [fn(x, y), z, t, t]
```