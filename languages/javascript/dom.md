## Basics
`document.createElement("p")` &rarr; creates new element

`document.getElementById("id")` &rarr; get one element by id

`document.querySelector("#btn")` &rarr; finds first element matching id/class. must provide operator (.myclass)

`element.classList.add("Name1", "Name2")` &rarr; adds new classes to element

`element.classList.remove("Name1")` &rarr; removes classes from element

`element.id = "something"` &rarr; sets id attribute of element

`parent.appendChild(element)` &rarr; adds element as parent elements last child

`element.className = "Name1 Name2 Name3"` &rarr; sets entire class string as given (removes old)

## Timeouts
`setTimeout(()=>{},2000)` &rarr; run once after the delay

`clearTimeout(id)` &rarr; clears the timeout timer

`setInterval(()=>{},2000)` &rarr; runs repeatedly after delay

`clearinterval()` &rarr; clears the interval timer

```js
// example
const id = setInterval(fn, 1000);
clearInterval(id);
```

## Setting Texts
`element.textContent` &rarr; shows all text including sub-tags and secrets w/o tags (preferred way)

`element.innerText` &rarr; shows the visible text to the user on browser w/o tags

`element.innerHTML` &rarr; shows the visible text with tags

`input.value` &rarr; used for getting value of input fields like `input, textarea, select`

## EventListeners
`btn.addEventListener("event",(e)=>{})` &rarr; event listener method

`e.key` &rarr; character/symbol ("a")

`e.code` &rarr; physical key name ("KeyA")

```js
// other events
click
mouseover
keydown
submit
load
resize
```

## Window
`window.location.reload();` &rarr; reloads current page

`window.location.href = "path";` &rarr; navigates to page with back button accessible

`window.location.replace("path");` &rarr; navigates to page but no back button is acessible

## Startup
`document.fonts.ready.then(()=>{});` &rarr; run after fonts load

```js
// runs after page, images, fonts, everything loads
// old unsafe version
window.onload = ()=>{}; 

//newer better version
window.addEventListener("load", () => {});
```
## Popups
`alert("message")` &rarr; execution pauses until user clicks okay

`prompt("message")` &rarr; gives a input box to fill.

```js
const name = prompt("Enter name:");

if (name) {
  console.log("Hello", name);
}
```

