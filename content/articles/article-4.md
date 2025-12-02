---
title: "Article Two"
description: ""
omit_header_text: true
summary: "Another programming article."
type: page
weight: 3
---

## Article Two: 

## Introduction to the Problem: 

This homework problem is from chapter two. It asks to write a program that creates a string that represents an 8×8 grid, using newline characters to separate lines. At each position of the grid there is either a space or a "#" character. 
The characters should form a chessboard.

Passing this string to console.log should show something like this:

```js
 # # # #
# # # # 
 # # # #
# # # # 
 # # # #
# # # # 
 # # # #
# # # #
```
It also asks that when you have a program that generates this pattern, define a binding size = 8 and change 
the program so that it works for any size, outputting a grid of the given width and height.

## Breaking Down the Solution: 

The first line of the solution creates a constant value called size. It will stay 8 the entire time and control how tall and wide the grid will be.

```js
const size = 8;
```

The second line of code makes an empty string called board. This is what will build the chessboard pattern by adding characters to this string.

```js
let board = "";
```

The next chunk of code is a for loop. This for loop will help to create the rows in the pattern. It follows the for loop steps of initialization, check, and update.

```js
for (let y = 0; y < size; y++)
```

Initialization (let y = 0): A binding y is created and initialized to 0. This binding tracks the current row number.

Check (y < size): The loop continues running as long as the current row index (y) is less than the defined size (8).

Update (y++): After the body of the loop runs, the y binding is incremented by 1.


The next line of code is another for loop that helps to create the columns in the pattern

```js
for (let x = 0; x < size; x++)
```

This line runs like the previous for loop, just with the columns instead. It follows the for loop steps of initialization, check, and update.

It starts x at 0, keeps going while x is less than size, and adds 1 to x each time. The variable x keeps track of which column you're on.

The next line of code is an "if, else" conditional statement, 

```js 
if ((x + y) % 2 == 0) {
  board += " ";
} else {
  board += "#";
}
```

This "if, else" conditional statement helps the pattern to choose a "#" character or a space to create the checkerboard pattern.
```js
(x + y) % 2 
```
checks whether the sum of the row and column numbers is even. If it’s even, it adds a space " ". If it’s odd, it add a "#". This creates the alternating pattern needed for a chessboard.

After the inner loop and "if, else" statement finishes a full row, the next line of code adds a newline character so the next row starts on a new line.

```js
board += "\n";
```

The final line of code prints the checkerboard pattern to the console. 

```js
console.log(board);
```

## Full Solution

The full solution looks like this:

```js
const size = 8;
let board = "";

for (let y = 0; y < size; y++) {
  for (let x = 0; x < size; x++) {
    if ((x + y) % 2 == 0) {
      board += " ";
    } else {
      board += "#";
    }
  }
  board += "\n";
}

console.log(board);
```

This solution was found through Chapter Two in Eloquent JavaScript by Homer White and explinations/help given during class lectures. 



