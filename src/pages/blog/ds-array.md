---
layout: "../../layouts/BlogPost.astro"
title: "Data Structure: Array"
pubDate: "Jul 15, 2022"
---

Array is a collection of items that stored at contiguous memory location, its a static linear non-primitive data structure, the purpose of array is to store multiple element of the same type. Each item of the array is commonly called ‘element of array’, and every element has its own index of its sequence where you can use it as a key to peek the element you want to see, the indexes start from zero or also known as zero base.

![memory location](/blog/ds-array/image.png)

Array has a fixed size/length, means that you can’t add elements more than its size, when you try to add more, stack overflow will occur. Array also can be used to implement other data structure like stack and queue.

Here’s a sample implementation of array in Go

```javascript
// we declare an array of string type and set its length/size to 3
var actors [3]string

// assign every element of the array with values
actors[0] = "Keanu Reeves"
actors[1] = "Robert Downey Jr."
actors[2] = "Leonardo DiCaprio"

// try to reach item of actors variable that has index of 1
fmt.Println(actors[1]) // Robert Downey Jr.
```