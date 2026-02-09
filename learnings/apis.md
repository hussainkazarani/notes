## API Basics
> \- set of **endpoints** and **rules** to let programs intereact with each other other. <br>
> \- **endpoints** &rarr; `GET /api/users`, `POST /api/users` <br>
> \- **rules** &rarr; they are what the endponts follow as guidelines (ex: send JSON Data) <br>
> \- in short it's a way for frontend client and backend server to communicate

## REST APIs (Representational State Transfer)
> \- REST is an **architectural style** for designing APIs using HTTP methods, URLs (paths), Patterns <br>
> \- we use HTTP methods like: <br>
> &nbsp;&nbsp;&nbsp; `GET` &rarr; read data <br>
> &nbsp;&nbsp;&nbsp; `POST` &rarr; create <br>
> &nbsp;&nbsp;&nbsp; `PUT/PATCH` &rarr; update <br>
> &nbsp;&nbsp;&nbsp; `DELETE` &rarr; remove
>
> \- Uses resource-based URLs (nouns, not verbs) <br>
> \- examples are: `/api/users/`, `api/users/42`
>
> \- they are stateless requests. each request contains all info needed <br>
> \- standard status codes like `200, 201, 404, 401, etc`

```js
// examples
GET  /api/users        // list users
GET  /api/users/42     // get one user
POST /api/users        // create user
DELETE /api/users/42   // delete user
```

## Cookies
> \- they are small `key-value data` stored in the browser and automatically sent back to the server with matching requests. <br>
> \- used for:  `login state, preferences, tracking, session IDs` <br>
> \- key things to remember are: <br>
> &nbsp;&nbsp;&nbsp; stored on client (browser) <br>
> &nbsp;&nbsp;&nbsp; sent via headers automatically <br>
> &nbsp;&nbsp;&nbsp; set by server using Set-Cookie <br>
> &nbsp;&nbsp;&nbsp; can have flags like `HttpOnly` (JS cannot read it), `Expires/Max-Age` (when to delete) 

```js
// example
Set-Cookie: theme=dark; Max-Age=3600; HttpOnly
```

## Sessions
> \- they are **server-side stored user state** tied to a session ID <br>
> \- how they work: <br>
> &nbsp;&nbsp;&nbsp; 1\. server creates session data (user_id, auth, cart, etc.) <br>
> &nbsp;&nbsp;&nbsp; 2\. server generates a session ID <br>
> &nbsp;&nbsp;&nbsp; 3\. session ID is sent to browser (usually via cookie) <br>
> &nbsp;&nbsp;&nbsp; 4\. browser sends that ID back each request <br>
> &nbsp;&nbsp;&nbsp; 5\. server looks up the stored session data <br>
> \- key things to remember are: <br>
> &nbsp;&nbsp;&nbsp; stored on server <br>
> &nbsp;&nbsp;&nbsp; more secure for sensitive data <br>
> &nbsp;&nbsp;&nbsp; cookie only holds the session ID, not the actual data <br>
> &nbsp;&nbsp;&nbsp; expires after inactivity or time limit <br>

```js
// example
1. browser  // login
2. server   // creates session + sends cookie: session_id=abc123
3. browser  // sends session_id on every request
4. server   // loads session data using that ID
```