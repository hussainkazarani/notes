## Commands
`ffmpeg -i input.gif -vf "fps=12,scale=480:-1" output.webp` &rarr; GIF to WEBP

`ffmpeg -i input.webm -vf "fps=12,scale=480:-1" -loop 0 output.webp` &rarr; WEBM to WEBP

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