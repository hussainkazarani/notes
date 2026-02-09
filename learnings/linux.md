## Linux Basics
### Package Management (apt)
`apt` = Debian/Ubuntu package manager. It installs and updates software

```bash
apt update          # refresh package list
apt upgrade         # upgrade installed packages
apt install pkg     # install package
apt install -y pkg  # auto-yes to prompts
apt clean           # clear package cache
```

### File & Directory Commands
```bash
ls            # list files
ls -l         # long format
ls -a         # include hidden
ls -A         # hidden except . and ..
ls -la        # combo

cd /path      # change directory
cp a b        # copy file
mv old new    # move/rename
```
### Downloading Files
> \- both are used to pull data from a URL. the difference is in intent and default behavior <br>

**wget** &rarr; just download the file <br>
```bash
# example
wget https://example.com/file.zip

# downloads it
# saves to current folder
# uses same filename automatically
# built for downloading stuff
```

**curl** &rarr; make a request and show the response 

`curl` = API testing + scripting + headers + methods.

```bash
# use to talk to a server / API
curl https://example.com

# sends HTTP request
# prints response to terminal
# does not save file unless told

# to save file and other stuff
curl -O https://example.com/file.zip
curl -X POST https://api.site.com/users
curl -H "Authorization: Bearer TOKEN" URL
curl -d '{"name":"test"}' URL
```

### Archiver
```bash
tar -xvf file.tar
```
**Common flags:** <br>
x = extract <br>
v = verbose <br>
f = file

**For gzip:**
```bash
tar -xzvf file.tar.gz
```

### Service
```bash
# old style
service <name> <operation>

# new style
systemctl <operation> <name>

# example
systemctl start nginx
systemctl stop nginx
```

**operations** &rarr; start, stop, restart, status, enable/diable (start/stop at boot)

### Echo
```bash
# print text
echo "hello"
# write into files
echo "data" > file.txt
```
