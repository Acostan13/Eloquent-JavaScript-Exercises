# Chapter 2: Program Structure


## 2.1 Looping a triangle

Write a loop that makes seven calls to console.log to output the following triangle:

```javascript
#
##
###
####
#####
######
#######
```

#### Solution

```javascript
let counter = '#'

for(i=0;i<6;i++){
  console.log(counter)
  counter+= "#"  
}
```

## 2.2 FizzBuzz

Write a program that uses console.log to print all the numbers from 1 to 100, with two exceptions. For numbers divisible by 3, print `Fizz` instead of the number, and for numbers divisible by 5 (and not 3), print `Buzz` instead.

When you have that working, modify your program to print `FizzBuzz`, for numbers that are divisible by both 3 and 5 (and still print `Fizz` or `Buzz` for numbers divisible by only one of those).

#### Solution

```javascript
for (i=1; i<=100; i++) {
    if (i % 5 ===0 && i % 3 ===0) {
        console.log('FizzBuzz')
    } else if ( i % 3 ===0) {
        console.log('Fizz')
    } else if ( i % 5 ===0) {
        console.log('Buzz')
    } else {
        console.log(i)
    }
}
```

## 2.3 Chess board

Write a program that creates a string that represents an 8×8 grid, using newline characters to separate lines. At each position of the grid there is either a space or a `#` character. The characters should form a chess board.

Passing this string to `console.log` should show something like this:

```javascript
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
 # # # #
# # # #
```
When you have a program that generates this pattern, define a variable `size = 8` and change the program so that it works for any `size`, outputting a grid of the given width and height.

#### Solution

```javascript
let size = 8
let chessBoard = ""

// Outer Loop iterates through each row
for(i=1;i<size;i++){
  // Inner Loop adds ' ' or '#' to each row
  for(j=0;j<size; j++){
    // Adds an even number of spaces and hashes
    if((j+i) % 2 === 0){
      chessBoard += "#"
    } else {
      chessBoard += " "
    }
  }
  // Adds a newline character to start the next row
  chessBoard += "\n"
}

console.log(chessBoard)

```
