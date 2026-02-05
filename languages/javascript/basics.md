## Basics
### Loops
```js
let items = [1, 2, 3, 4];

// normal for loop
for (let i = 0; i < items.length; i++) {}

// item iterates through all items with dot operator
items.forEach((item)=>{});

// simpler for loop
for(let item of items){}
```

### Arrays
```js
const arr = [1, 2, 3];
arr.push(4);
arr.includes(2); // true or false
arr.length;
arr.find((item)=>{item.name=="iPhone"});
arr.splice(startIndex, length);
```

### Map
```js
const map = new Map();
map.set("key", "value");
map.get("key");
map.delete("key");
```

### Date
```js
const date = new Date();
date.getFullYear();
date.getMonth();
date.getDate();
date.toString();
```

### Random
`Math.random()` &rarr; between 0 and 1 <br>
`Math.floor(math.random()*10)` &rarr; between 0 and 9

### Other
```js
console.log("5" == 5); // loose equality as type is converted [true]
console.log("5" === 5); // strict equality as type is not converted [false]
```

`/` &rarr; absolute path from root <br>
`./` &rarr; current folder <br>
`../` &rarr; one level up (parent folder)

`element.toString()` &rarr; turns element into string <br>
`JSON.stringify(obj)` &rarr; Javascript Object to JSON String <br>
`JSON.parse(json)` &rarr; JSON String to Javascript Object <br>
`querystring.parse(query)` &rarr; Query String to Javascript Object
```js
// old way
querystring.parse("name=Hussain&age=20")
// Output - { name: "Hussain", age: "20" }

// modern way
const params = new URLSearchParams(location.search);
params.get("name");
```


## Functions
```js
function name() {} // normal function
() => {} // arrow function
const name = () => {}; // arrow function with variable name

```

## Strings
`"hello".match(/ll/)` &rarr; string regex for matching

```js
// strings
let text = 'hello';
let text = "Hello";
let text = `hello`; ✅ // backtick option available in javascript (multi-line)
// string interpolation
console.log(`Hello ${variable}`); // `${variable}` in javascript
typeof text // type in javascript is 'string'
```
