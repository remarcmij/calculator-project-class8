# Standardized execute()

In order to enable cross-project unit tests and programmability we need the various projects to standardize on the way the calculator functions can be invoked. This document proposes such a standard.

## Stack representation

The standard four-register RPN stack should be represented by a property on your application state named `stack`. So the `initialState` in your app should look like:

```js
{
    stack: [0, 0, 0, 0],
    // other state properties
}
```

The mapping of array elements to the `x`, `y`, `z` and `t` values should be standardized, such that `x` maps to `stack[0]`, `y` to `stack[1]` etc.

This allows us to destructure and reconstruct the stack as outlined in [_RPN stack_](https://github.com/remarcmij/calculator-project-class8/blob/master/RPN%20stack.md) document.

## execute() function

This standardized function takes your application state and a key code as parameters and should produce a new state as a result of processing the passed key code.

```
const newState = execute(state, keyCode)
```

You should `export` this function from which ever module it is defined. This function has the form of a `reducer`, i.e. a function that can readily be used by the `Array.reduce()` method. This enables the execution of a series of keystrokes to form a simple 'program' to be run by your calculator, like in this example:

```
const keyCodes = [ ... ] // define a series of keystrokes here
const finalState = keyCodes.reduce(execute, initialState)
```

See also the [_Rydberg constant_](https://github.com/remarcmij/calculator-project-class8/blob/master/Rydberg%20constant.md) and the file `rydberg.test.js` in this repo.

## Standardized key codes

We need to standardize the key codes that we emit from our keyboard components into the calculating engine (i.e. the `execute` function). The file `keyCodes.js` in this repo represents a proposed standard set of key codes as a series of string constants. Please prefer the use of the symbolic names for the constants over the actual string values wherever you can.


