## `dotenv` Package
`dotenv` loads environment variables from a .env file into your Node.js app

### Usage
1. install dotenv &rarr; `npm install dotenv`

2. at the top of your entry file, add:
    ```js
    import dotenv from "dotenv";
    dotenv.config();
    ```

3. use the variables as shown: `console.log(process.env.PORT);`

the config parameter takes an `options object` which is as follows:

```js
dotenv.config({
  path: "../.env",
  encoding: "utf8",
  override: true //overrides the current .env
});
```

## Node Flag
```js
// --env-file flag
node --env-file=.env app.js
```