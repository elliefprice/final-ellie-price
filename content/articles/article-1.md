---
title: "Article One"
description: ""
omit_header_text: true
summary: "Another programming article."
type: page
weight: 3
---

## Article One:

## Introduction to the Problem
 
This homework problem is from chapter two. The problem asks to write a loop that makes seven calls to console.log to output the following triangle:

```js
#
##
###
####
#####
######
#######
```
## Breaking Down the Solution

The first line of code to the solution creates a binding named "triangle" (let) and assigns the value of an empy string to it (" "). 

```js
let triangle = "";
```

The second line of code creates a for loop. This for loop has three main parts:  initialization, check, and update.

Initiation: 

```js
let triangle = "#"
```

This creates an inner binding (also named triangle). This new variabe is created inside the loop, and it starts out as the “#” symbol (a single character).

Check:

This code line decides whether the loop should keep going. The loop continues as long as the triangle string has 7 or fewer characters, while the "triangle.length" property tells how many characters are in the string (7).

```js
triangle.length <= 7
```

Update:

```js
console.log(triangle)
```

This code line prints the current triangle string.

Then the loop updates:

```js
triangle += "#"
```

This code line adds one more "#" to the end of the triangle string.

The code builds a triangle pattern by printing a string that gets one "#" longer each time the loop runs, up to seven times. while the last line prints the result to the console.

```js
console.log(triangle)
```
## Full Solution 

The full solution looks like this:

```js
let triangle = "";

for (let triangle = "#";
    triangle.length <= 7;
    triangle += "#") {
        console.log(triangle);
    }
console.log(triangle)
```

This solution was found through Chapter Two in Eloquent JavaScript by Homer White and explinations/help given during class lectures. 