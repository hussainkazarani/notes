## Functions
```js
function name() {} // normal function
() => {} // arrow function
const name = () => {}; // arrow function with variable name

```

## Strings
```js
// strings
let text = 'hello';
let text = "Hello";
let text = `hello`; ✅ // backtick option available in javascript (multi-line)
// string interpolation
print(`Hello ${variable}`); // `${variable}` in javascript
typeof text // type in javascript is 'string'
```

## Errors and Exceptions
`Error` &rarr; the object type

`Exception` &rarr; event of something being thrown. it stops execution and runs its catch block

`Try/Catch` &rarr; 
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