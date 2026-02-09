## Basics
axios is a JS library/package to make HTTP requests. better then fetch as it has many extra features like error handling, JSON auto-transform, interceptors, etc...

it does not build APIs only consumes them

`Frontend` &rarr; CDN Scripts

`Backend` &rarr; `npm install axios`

## Example
```js
import axios from "axios";

// complete structure
axios({
  method: "post",
  url: "https://api.example.com/users",
  data: { name: "Hussain" },
  params: { admin: true },
  headers: {
    Authorization: "Bearer TOKEN"
  },
  timeout: 5000
}); // returns promise

```

## HTTP Methods
```js
axios.get(url, config)
axios.post(url, data, config)
axios.put(url, data, config)
axios.delete(url, config)
axios.patch(url, data, config)
```

```js
// GET - fetch data
const res = await axios.get("http://localhost:3000/users");
console.log(res.data);

// POST - send data
await axios.post("http://localhost:3000/users", {
  name: "Hussain",
  age: 22
});

// PUT - replace/update data
await axios.put("/users/5", {
  name: "Updated"
});

// PATCH - partial update
await axios.patch("/users/5", {
  name: "Small change"
});

// DELETE - delete data
await axios.delete("/users/5");
```

## Response Object
```js
const res = await axios.get("/users"); // response object

res.data        // actual data from server
res.status      // 200, 404, 500, etc
res.headers
res.config
```

## Other Methods
### axios.all() &rarr; multiple calls at once
```js
const results = await axios.all([
  axios.get("/users"),
  axios.get("/posts")
]);

const users = results[0].data;
const posts = results[1].data;
```