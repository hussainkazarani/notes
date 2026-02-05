## HTML
```html
<form>
    <label for="name">Name</label>
    <input name="name" placeholder="Enter name">
    <button type="submit">Submit</button>
</form>
```

## Javascript
```js
const form = document.querySelector("form");
form.addEventListener("submit", function(e) {
    e.preventDefault() // stops normal form submission
    const formData = new FormData(form); // get all fields
    const name = formData.get("name");
})
querystring.parse() // data gotten on submit needs to be parsed
```

## Form Fields
`<form>` &rarr; container for all the data

`<label>` &rarr; refers to the text that is inline to the input box. needs a `for` property if we want clicking on label to trigger input

`<input>` &rarr; where i get the data from. \***must**\* have a `name` property. can also have `id` property to target the input for css

`type` &rarr; different types of data

> the `name` property maps to the `formData.get()` property

```js
// input types
text
password
email
url
tel
number
range // <input type="range" min="0" max="100">
date
checkbox // value sent only if checked
radio // <input type="radio" name="color" value="red">

// button types
submit
reset

// other types
<textarea name="bio"></textarea>

<select name="country">
  <option value="IN">India</option>
  <option value="US">USA</option>
</select>

// other properties inside input
placeholder, required, checked, disabled, readonly, value

```