## Use Cookies
yt-dlp --cookies cookies.txt "https://fast.wistia.com/embed/medias/d5nz8uc6vj.m3u8"

## Basic Commands
Normal Command : `yt-dlp "URL"`
<!-- bv is best-video -->
Only Video : `yt-dlp  -f bv "URL"`
<!-- Audio only in mp3 -->
Only Audio : `yt-dlp -x --audio-format mp3 "URL"` OR `yt-dlp -f AUDIO_ID -x "URL"`

## Extra Commands
Available Formats : `yt-dlp -F "URL"`

Use Format : `yt-dlp -f VIDEO_ID+AUDIO_ID "URL"`

Use a User-Agent : `yt-dlp --user-agent "Mozilla/5.0" "URL"`

```bash
# other way
yt-dlp --impersonate chrome "URL"
yt-dlp --impersonate firefox "URL"
yt-dlp --impersonate safari "URL"
```


Download a Playlist : `yt-dlp "PLAYLIST_URL"`

Download all from a TXT File : `yt-dlp -a list.txt`

Rename File/Folder : `yt-dlp -o "%(title)s.%(ext)s" "URL"` AND `yt-dlp -o "%(uploader)s/%(title)s.%(ext)s" "URL"`

> \- Keywords may include stuff like application/x-mpeg