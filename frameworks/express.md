## Basics
### CommonJS
```js
const express = require("express");
const app = express();
app.listen(8000,() => { console.log('Server running...') });
```
### ESModules (Better)

### Send APIs
```js
app.get('/api/posts', (req, res)=>{
    res.send(posts); // or res.json(posts)
});
```

### Load Pages
```js
res.sendFile(path.join(__dirname__, 'public', 'index.html'));
```

## Route vs Controller
```js
// controller
/**
 * @route GET /users
 * @desc Get all users
 * @access Public
 */
const getPosts = (req, res) => {
  res.send("Posts list");
}

// route
app.get("/users", getPosts);
```

### Routes
```js
// auto convert to correct format internally 
app.get('/',(req,res,next)=>{
    let msg1 = '<h1>Hello</h1>';
    let msg2 = {message:'Hello'};
    res.send(msg1) 
})
```

### Controllers
#### Tags and Conventions
convention is as follows:
```js
/**
 * @route GET /users
 * @desc Get all users
 * @access Public
 */
```

the different tags are as follows:
```js
@route
@method
@path
@desc
@summary
@access
@param
@returns
```

#### Controller Example
```js
/**
 * @route GET /users
 * @desc Get all users
 * @access Public
 */
const getPosts = (req, res) => {
  res.send("Posts list");
}
```

## Misc
### Static Folders Setup
```js
// here the path is the same as folder path
app.use(express.static(path.join(__dirname__,'public')));
```

### Frontend Example
```js
const res = await fetch('https://example.com/api/posts');
if(!res.ok) throw new Error('idk');
```