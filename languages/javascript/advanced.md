## Classes and Objects
> javascript has `Javascript Objects` and these are different from `JSON object`. they can be converted into one another though

`public functions` &rarr; accessible anywhere <br>
`private functions (#)` &rarr; only accessible in class <br>
`static` &rarr; belongs to class not instance

```js
// classes
class Particle{
    constructor(){}
    update(){}
}
const utils = new MathStuff()
utils.addStuff(5, 3) // will not work if static
MathStuff.addStuff(5, 3) // will work for static

// constructor function pattern
// old school way before classes were introduced
function Circle(c,y){
    this.x = x;
    this.y = y;
    this.draw = function(){}
}
var circle = new Circle(10, 20);
```

```js
// javascript objects
const obj = {
    name: "John",
    age: 25
}
Object.keys(obj); // gives keys of object in string format ["name", "age"]
obj.name // directly calling js object value
obj["age"].value // only when the key has an object as its value
```

## Asynchronous
> JS does not block the program when executing async operations. it will continue to run other tasks when this is doing its work in the background

> `Promise` &rarr; its an object that represents a future result. aka its a placeholder for the value that will come. it has 3 states: `pending, resolved, rejected`. `reject` is not auromatically called we need to write logic for it

> remember that on rejection `await` will also throw error

> 2 ways to write promises: `then/catch` or `try/catch with await/async`

```js
// example
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    const ok = Math.random() > 0.5;

    if (ok) {
      resolve(42);
    } else {
      reject(new Error("bad luck"));
    }
  }, 1000);
});

// right now - no value
// after 1 second - will give 42 or error
```

### Callback
> it is a function you give to a function to call later

```js
// examples
setTimeout(()=>{}, 1000);
btn.addEventListener('click', ()=>{});
```

### Promises
```js
// then/catch
p.then(value => {console.log(value);})
 .catch(err => {console.error(err);});
```

### Async/Await
```js
// await/async with try/catch
try {
  const value = await p;
  console.log(value);
} catch (err) {
  console.error(err);
}
```

## Fetch
> learn after you know async/await and promises. fetch sends a http request and responds with a promise for the future data. it returns a `Response Object`. not JSON, not data.

```js
// fetch skeleton
const response = await fetch(url);
if(!response.ok) throw new Error("HTTP error");
const data = response.json();
```

```js
// get data
try {
    const res = await fetch("https://example.com/api/posts");
    if (!res.ok) throw new Error("Failed");
    const data = await res.json();
    console.log(data);
} catch (err) {
    console.error(err);
}

// post data
await fetch("https://example.com/api/posts", {
  method: "POST",
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify({
    title: "Hello"
  })
});
```
### Response Object Methods
`res.json()` &rarr; JSON String to Javascript Object

### Data Conversion Utilities
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

## Errors and Exceptions
`Error` &rarr; JS object type describing failure `new Error()`

`Exception` &rarr; event of something being thrown. it stops execution and runs its catch block `throw error`

`Try/Catch` &rarr; catch thrown errors and handle them safely `try{ } catch(err){ }`. 

`console.error` &rarr; console log in red. its the convention for errors `console.error("failedd")`
> the `err` variable contains the thrown value and can be accessed via `err.message` while `err.value` contains error type name
```js
try {
  const res = await fetch('https://example.com/api/posts');
  if (!res.ok) throw new Error("Bad response");
  const data = await res.json();
  console.log(data);
} catch (err) {
  console.error("Caught error:", err.message);
}
```