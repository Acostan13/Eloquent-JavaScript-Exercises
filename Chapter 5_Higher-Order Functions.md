# Chapter 5: Higher-Order Functions


## Flattening

Use the `reduce` method in combination with the `concat` method to “flatten” an array of arrays into a single array that has all the elements of the original arrays.

#### Solution
```javascript
let arrays = [[1, 2, 3], [4, 5], [6]]

console.log(arrays.reduce((a,b) => a.concat(b), []))
// → [1, 2, 3, 4, 5, 6]
```

## Your own loop

Write a higher-order function loop that provides something like a for loop statement. It takes a value, a test function, an update function, and a body function. Each iteration, it first runs the test function on the current loop value and stops if that returns false. Then it calls the body function, giving it the current value. Finally, it calls the update function to create a new value and starts from the beginning.

#### Solution

```javascript
loop = (start, test, update, body) => {
  for(value = start; test(value); value = update(value)) {
    body(value)
  }
}

loop(3, n => n > 0, n => n - 1, console.log);
// → 3
// → 2
// → 1
```

## Everything

Analogous to the some method, arrays also have an `every` method. This one returns true when the given function returns true for *every* element in the array. In a way, `some` is a version of the `||` operator that acts on arrays, and `every` is like the `&&` operator.

Implement `every` as a function that takes an array and a predicate function as parameters. Write two versions, one using a loop and one using the some method.
#### Solution

```javascript
// Using For Loop
every = (array, test) => {
  for(let element of array){
    if(!test(element)) return false
  }
  return true
}

// Using .some Method
every = (array, test) => {
  return !array.some(element => !test(element))
}

console.log(every([1, 3, 5], n => n < 10))
// → true
console.log(every([2, 4, 16], n => n < 10))
// → false
console.log(every([], n => n < 10))
// → true
```

## Dominant writing direction

Write a function that computes the dominant writing direction in a string of text. Remember that each script object has a `direction` property that can be `"ltr"` (left to right), `"rtl"` (right to left), or `"ttb"` (top to bottom).

The dominant direction is the direction of a majority of the characters that have a script associated with them. The `characterScript` and `countBy` functions defined earlier in the chapter are probably useful here.

#### Solution
```javascript
dominantDirection = (text) => {
  let counted = countBy(text, char => {
    let script = characterScript(char.codePointAt(0))
    return script ? script.direction : "none"
  }).filter(({name}) => name != "none")

  if (counted.length == 0) return "ltr";

  return counted.reduce((a, b) => a.count > b.count ? a : b).name
}

console.log(dominantDirection("Hello!"))
// → ltr
console.log(dominantDirection("Hey, مساء الخير"))
// → rtl
```