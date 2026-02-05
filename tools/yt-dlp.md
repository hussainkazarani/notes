## Use Cookies
yt-dlp --cookies cookies.txt "URL"
> can download videos which have extensions like m3u8, mp4

## Basic Commands
`yt-dlp "URL"` &rarr; normal command

`yt-dlp "PLAYLIST_URL"` &rarr; download a playlist

`yt-dlp -a list.txt` &rarr; download all from a TXT file

`yt-dlp  -f bv "URL"` &rarr; only video (bv = best-video)

```bash
# Audio only in mp3
yt-dlp -x --audio-format mp3 "URL"
yt-dlp -f AUDIO_ID -x "URL"
```

## Extra Commands
`yt-dlp -F "URL"` &rarr; available formats

`yt-dlp -f VIDEO_ID+AUDIO_ID "URL"` &rarr; use a particular format

```bash
# using a user-agent 
yt-dlp --user-agent "Mozilla/5.0" "URL"
yt-dlp --impersonate chrome "URL"
yt-dlp --impersonate firefox "URL"
yt-dlp --impersonate safari "URL"
```
```bash
# renaming a file/folder
yt-dlp -o "%(title)s.%(ext)s" "URL"
yt-dlp -o "%(uploader)s/%(title)s.%(ext)s" "URL"
```

> \- keywords may include stuff like application/x-mpeg<br>
> \- can install from wistia