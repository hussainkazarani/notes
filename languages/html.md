## Linking
```html
<head>
    <link rel="stylesheet" href="styles.css" />
</head>
<body>
    ...
    <script src="script.js"></script>
    <script type="module" src="script2.js"></script>
</body>
```
## Other Tags
```html
<!-- canvas -->
<canvas></canvas>

<!-- website hyperlinks -->
<a href="...">Google</a>
<a href="..." target="_blank" title="..."></a>

<!-- image -->
<img src="shrek.png" hright="300px" width="300px">

<!-- lists -->
<!-- unorderded -->
<ul>
    <li>...</li>
</ul>

<!-- ordered -->
<ol type="A">
    <li>...</li>
</ol>

<!-- description -->
<dl>
    <dt>...</dt>
    <dd>...</dd>
</dl>
```

## Tables
`colspan` &rarr; horizontally combines table cells
`rowspan` &rarr; vertically combines table cells

```html
<table>
    <tr colspan="2" rowspan="3">
        <th>...</th>
        <th>...</th>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
    </tr>
</table>
```

`<table border="1">` &rarr; basic border (not good looking) and has double borders

> we add inline CSS to remove double border and add a normal border <br>
> 1\. remove double border &rarr; `border-collapse: collapse;` <br>
> 2\. show border &rarr; `border="n"` <br>
> so we write it as ` <table border="n" style="border-collapse: collapse;">` <br>
> we can also add `text-align: center;` to style the table

## Forms
> More form details [here](../learnings/forms.md) (learning/forms.md)
```html
<form>
    <input type="text" name="firstname">
</form>
```

`name` &rarr variable name send to server

`id` &rarr; used to get value on frontend

`for` &rarr; connect label to input field (clicking on text highlights input)

> `for` and `id` connect a \<label> to an \<input> <br>
> `name` attribute is the part that makes radio buttons behave like a group instead of a bunch of independent chaos buttons.

```html
<!-- for and if are basically the same thing -->
<label for="sermon">Hey: </label>
<input type="text" id="sermon">
```

```html
<!-- types of input -->
text, number, email, reset, submit, password, radio

<!-- other attributes -->
min, max, maxlength, value, placeholder, required

<!-- radio - must have same name group and different values -->
<!-- example -->
<label>
    <input type="radio" name="choice" value="B"> Option B
</label>

<label>
    <input type="radio" name="choice" value="C"> Option C
</label>


<!-- select -->
<select name="payment">
    <option value="...">Hi</option>
</select>
```

## Form action and Method
> `action` and `method` tell the browser **where** to send the **form** and how to send it when the user clicks **submit**

```html
<!-- skeleton -->
<form action="/submit" method="post">
  ...
</form>

<!-- action is destination -->
<!-- here data goes to the `/submit` api -->
<form action="/submit">

<!-- method is how to send -->
<form method="get">
<form method="post">
```

> \- `GET` &rarr; data goes to url and shows in address bar
> (example: `/submit?color=blue&size=large`) <br>
> \- `POST` &rarr; data goes to body request and not shown in url address bar <br>
> \- can get the data using `req.body.username`. must also handle route

```js
// example backend in express
app.post('/submit', (req,res)=>{
    let username = req.body.username;
    res.send("Got the data: " + username);
});
```


