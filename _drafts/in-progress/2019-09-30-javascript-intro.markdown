---
published: false

layout: post
title: Javascript Notes
date: 2019-09-30
description: For beginners JS
img:  # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [javascript]
---

# Javascript

3 languages in browser
- html is markup
- css is syling
- javascript is a programming languages- the only programming language that can be executed in browser

Javascript is the only programming language able to be executed on the client side (python, etc are all server-side programming language)

History of javascript
- jQuery (2006)
  - first major JS library, allowed ppl to easily interact w the browser with a nicer user-friendly syntax to manipulate the browser
- NodeJS (2009)
  - allowed ppl to write JS on the server side (on the backend as well as the frontend)
  - since NodeJS, JS has become a fullstack languages
- Angular(2010), React (2013), View(2014)
  - continue to push JS forward

  talking about fonrt end : console is in the browser
  talking about the back end: consol is in the terminal

# JavaScript Data Types
- Numbers, strings, booleans
- null, undefined
- Objects (similar to a python array or list)

# variables
const & let
- creating a variable with const is like putting an object in a box
- with const, you cannot reassign a variable. With let, you can
const firstName = "Shannon";
console.log(firstName)

# conditional
three equal signs, must match EXACTLY
- absolute comparisions
two equal signs, the data type does not matter
let number = "7"
if (number == 7){
do something
}


jsbin.com

// // console.log(typeof 7)
// // console.log(typeof "shannon")
// // console.log(typeof true)

// const firstName = "Shannon";
// const lastName = "Gross"
// // concatination of strings
// console.log("Dear " + firstName + " " + lastName)

// // Conditions (if, else)
// let weather = "sunny"
// let temp = 190

// if (weather ===!"rainy") {
//   console.log("cancel the beach")
// } else if (weather ==="sunny"){
//   console.log("take the sunnies")
// } else {
//   console.log("No idea what to do")
// }

// // Boolean algebra &&, ||, !

// const nameOne = "Bob"
// const nameTwo = "Nob"
// const nameArray = [nameOne, nameTwo]

// nameArray.forEach((name) => {
//   if (name[0] === "B") {
//     console.log(name)
//   }
// });

// LOOPS
const students = ["john", "paul", "ringo"];
// console.log(students.length)

for (let i=0; i< students.length; i +=1){
     console.log(i + students[i]);
     }

students.forEach((student)=>{
  console.log(student[0])
})

function findBNames(myarray){
  myarray.forEach((name)=>{
    if (name[0] === "B") {
      return name
    }});}


mynewnames=["Bill", "shannon", "Boe"]
findBNames(mynewnames);
