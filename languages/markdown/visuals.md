## Downloads
GIFS [here.](https://giphy.com/explore/)

curl -L -o name.gif "https://media1.tenor.com/m/1k1tdO-A7MYAAAAC/ritsu-spin.gif"

## Videos
> Github cannot also do styles
```js
// aligns image to center
<p align="center"></p>

// clicking doesnt take to image
<a href="#"></a>

// can also use figcaptions
<figure>
    <img src="./assets/output1.webp" alt="Spinning Meme" width="50%">
    <figcaption>ritsu spinning like your cpu during ffmpeg</figcaption>
</figure>
```

```js
// in github
// videos
// 1. use Github Issues video
// 2. actual video (may not work)
  <video src="./assets/spin.webm" autoplay loop muted></video>

// images
// they must be cropped in correctly with infinite loops for gifs using ffmpeg
<p align="center"> 
  <a href="#">
  <figure>
    <img src="./assets/output1.webp" alt="Spinning Meme" width="50%">
    <figcaption>ritsu spinning like your cpu during ffmpeg</figcaption>
  </figure>
  </a>
</p>
```

## Corresponding Commands
```js
/*
tags are as follows:
-i <file> - take input
-vf "crop=w:h:x:y" - video filter
-c:v libwebp_anim - keep all frames
-loop 0 - infinite loop
*/
ffmpeg -i hello.gif -vf "crop=in_w:300:0:(in_h*0.20-175)" -c:v libwebp_anim -loop 0 output.webp
```
`ffmpeg -i input.gif output.webp` &rarr; GIF to WEBP

`<div align="center">my text here</div>` &rarr; centered text

## Images
align photos &rarr; [here](https://gist.github.com/DavidWells/7d2e0e1bc78f4ac59a123ddf8b74932d)