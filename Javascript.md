# JAVASCRIPT
## 1) Checking whether properties exist in the object or not.

```javascript
const user = {name: null, age:25};
```
#### Avoid using checks like this.
```javascript
if (user.name != null)
{
    console.log("name property exist");
}
// There may be the case when name is empty string or may be undefined so
// this check won't work.
```
#### Implement the check like this.
```javascript
if ("name" in user)
{
    console.log("Property exist")
}
// This will simply check wether the property exist in the json or not.
```

## 2) Generator function.
#### This type of function can be used for running tasks one by one.
```javascript
function* generatorFucntion() {
    console.log("Before 1");
    yield 1
    console.log("After 1, Before 2.");
    yield 2
    console.log("After 2, Before 3.");
    yield 3
    console.log("After 3");
}

const generator = generatorFucntion();
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
```
#### Output for the above code.
```bash
Before 1
{value: 1, done: false}
After 1, Before 2.
{value: 2, done: false}
After 2, Before 3.
{value: 3, done: false}
After 3
{value: undefined, done: true}
```

## 3) Importing module when necessary.
So i have two files one is my module(printModule.js) and another one is my main js.

printModule.js
```javascript
export default function printModule() {
    console.log("THis is in the module.");
}
```

main.js
```javascript
import printModule from './printModule.js';

printModule();

console.log("In main file");
```

#### Conditional import solution

Modify main.js like this.

```javascript
if (true) { // you can use your condition here
    import('printModule.js').then(({ default: printModule}) => {
        printModule();
    });
}

console.log("In main file");
```

## 4) Optional parameter check.
Sometimes the interanl property we are checking may be undefined and it throws exception in the console.
```javascript
const user = {
        name: "John Snow",
        address : {
            street : "XYZ Northway."
        }
    };
// so it may be possible that somtimes the street or address or user can be 
// undefined and you need to print street of the user.
// current solutions coders use like

console.log(user && user.address && user.address.street);
```

#### Modify your code like this.
```javascript
console.log(user?.address?.street);
// This will automatically checked the undefined variable to the end of the chain.
// This check also can be used for the functions. 
```

## 5) Freezing the object
So let's take an example.
```javascript
const user = {
    name: "John",
    age: 25,
    employeeId: 1022
};
// it is const but still you can modify the property like this.
user.name = "John Snow";
// This upper line is valid
```
Now modify the object like this.
```javascript
const user = Object.freeze({
    name: "John",
    age: 25,
    employeeId: 1022
});
// Now object freeze will freeze the object.
user.name = "John Snow";
// This time the upper line won't work.
// if you use 'use strict' this line will also throw the exceptio.
// Remember this won't work for the child json data you need to freeze that too.
```

## 6) How to check time consumed by the code.
#### Before
```javascript
const before = new Date();
for(let i = 0; i < 10000000000; i++){
    
}
const after = new Date();
console.log(after-before, "ms");
```
Output:-
```bash
9660 ms
```

#### When you know timer.
```javascript
console.time("note");
for(let i = 0; i < 10000000000; i++){
    
}
console.timeEnd("note");
// Here 'note' is the label for timer
```
Output:-
```bash
note: 9660.250732421875 ms
```

