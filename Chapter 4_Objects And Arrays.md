# Chapter 4: Objects And Arrays


## The sum of a range

Write a ```range``` function that takes two arguments, ```start``` and ```end```, and returns an array containing all the numbers from ```start``` up to (and including) ```end```.

As a bonus assignment, modify your ```range``` function to take an optional third argument that indicates the “step” value used when building the array. If no step is given, the elements go up by increments of one, corresponding to the old behavior. 
#### Solution

```javascript
// My Solution
range = (start, end, step) => {
  let arr = []
  let arrLength = Math.abs(end - start)

  if(step === undefined) {
    step = 1
  }
  
  if(step > 0){
    for(i=0;i<=arrLength;i+=step){
      arr.push(start)
      start+=step
    }
  } else {
    for(i=0;i<=arrLength;i-=step){
      arr.push(start)
      start+=step
    }
  }
  return arr
}

// Eloquent Solution
range(start, end, step = start < end ? 1 : -1) {
  let array = []

  if (step > 0) {
    for (let i = start; i <= end; i += step) array.push(i)
  } else {
    for (let i = start; i >= end; i += step) array.push(i)
  }
  return array
}

range(1, 10)
// → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
range(1, 10, 2)
// → [1, 3, 5, 7, 9]
range(5, 2, -1)
// → [5, 4, 3, 2]
```

Next, write a ```sum``` function that takes an array of ```numbers``` and returns the sum of these ```numbers```.

```javascript
sum = (nums) => {
  let total = 0
  for(num of nums){
    total += num
  }
  return total
}

sum(range(1, 10))
// → 55
```


## Reversing an array

Arrays have a `reverse` method that changes the array by inverting the order in which its elements appear. For this exercise, write two functions, `reverseArray` and `reverseArrayInPlace`. The first, `reverseArray`, takes an array as argument and produces a *new* array that has the same elements in the inverse order. The second, `reverseArrayInPlace`, does what the reverse method does: it *modifies* the array given as argument by reversing its elements. Neither may use the standard `reverse` method.

#### Solution

```javascript
reverseArray = (arr) => {
  let newArr = []
  for(i=arr.length-1; i>=0; i--){
    newArr.push(arr[i])
  }
  return newArr
}

reverseArray(["A", "B", "C"])
// → ["C", "B", "A"]


reverseArrayInPlace = (arr) => {
  for(i=0;i<Math.floor(arr.length / 2);i++){
    let tempArr = arr[i]
    arr[i] = arr[arr.length - 1 - i]
    arr[arr.length - 1 - i] = tempArr
  }
  return arr
}

reverseArrayInPlace([1, 2, 3, 4, 5])
// → [5, 4, 3, 2, 1]
```

## A list

Write a function `arrayToList` that builds up a list structure like the one shown when given `[1, 2, 3]` as argument. 
Also write a `listToArray` function that produces an array from a list. 
Then add a helper function `prepend`, which takes an element and a list and creates a new list that adds the element to the front of the input list, and `nth`, which takes a list and a number and returns the element at the given position in the list (with zero referring to the first element) or `undefined` when there is no such element.

If you haven’t already, also write a recursive version of `nth`.
#### Solution

```javascript
arrayToList = (arr) => {
  let list = null
  for(i=arr.length - 1; i>=0;i--){
    list = {value: arr[i], rest: list}
  }
  return list
}

arrayToList([1,2,3])
// → {value: 10, rest: {value: 20, rest: null}}

listToArray = (list) => {
  let arr = []
  console.log(list)
  for (let node = list; node; node = node.rest) {
    arr.push(node.value)
  }
  return arr
}

listToArray(arrayToList([10, 20, 30]))
// → [10, 20, 30]
```
```javascript
prepend = (value, list) => {
  return {value, rest: list}
}

nth = (list, n) => {
  if (!list) return undefined
  else if (n==0) return list.value
  else return nth(list.rest, n - 1)
}

prepend(10, prepend(20, null))
// → {value: 10, rest: {value: 20, rest: null}}
```

## Deep comparison

Write a function `deepEqual` that takes two values and returns true only if they are the same value or are objects with the same properties, where the values of the properties are equal when compared with a recursive call to `deepEqual`.

To find out whether values should be compared directly (use the === operator for that) or have their properties compared, you can use the `typeof` operator. 
If it produces "`object`" for both values, you should do a deep comparison. 
But you have to take one silly exception into account: because of a historical accident, `typeof` `null` also produces "`object`".
#### Solution
```javascript
deepEqual = (a,b) =>{
  if (a === b) return true
  
  if (a == null || typeof a != "object" ||
      b == null || typeof b != "object") return false

  let keysA = Object.keys(a)
  let keysB = Object.keys(b)

  if (keysA.length != keysB.length) return false

  for (let key of keysA) {
    if (!keysB.includes(key) || !deepEqual(a[key], b[key])) return false
  }

  return true
}

let obj = {here: {is: "an"}, object: 2}

deepEqual(obj, obj)
// → true
deepEqual(obj, {here: 1, object: 2})
// → false
deepEqual(obj, {here: {is: "an"}, object: 2})
// → true
```