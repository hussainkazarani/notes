## What is Bash?
- Bash = Bourne Again SHell
- Most commonly used Linux shell
- Shell scripting language
- Good for automation and quick scripts
- Comes preinstalled on most Linux systems
- Not OOP, limited compared to full languages

## Basic Commands
```bash
echo Hello        # print text
cat file.txt      # show file contents
pwd               # print working directory
echo $SHELL       # show current shell
```

## Running Bash Scripts
### Run without shebang (explicit interpreter)
```bash
bash script.sh
```

### With shebang (recommended)
a shebang is the first line in a script that tells the system to use a particular interpreter to run a file

```bash
#!/bin/bash
```

### Make script executable
```bash
chmod u+x script.sh
./script.sh
```

## Variables
```bash
NAME="Hussain"
echo $NAME

# no newline
echo -n "text"

# use variables
cp $SRC $DEST
User input:

read FIRST_NAME
echo $FIRST_NAME
```

## Positional Arguments
```bash
# arguments passed to script
./script.sh one two

inside script
$0  # script name
$1  # first argument
$2  # second argument

# example
echo $1 # output: two
```
> `$0` is reserved for shell

## Pipes
send output of one command to another
```bash
ls -l /usr/bin | grep bash
```

## Output Redirection
```bash
> file.txt     # overwrite
>> file.txt    # append
```
```bash
# example:
echo hello > hello.txt
echo world >> hello.txt
```

## Test Expressions
\- used to test expressions/variables. <br>
\- spaces are required inside brackets:
```bash
[ "$A" = "hello" ]
```

Exit status:
```bash
echo $?   # 0 = success, non-zero = failure
```

## if / elif / else
```bash
if [ "$1" = "herbert" ]; then
    echo "Match"
elif [ "$1" = "john" ]; then
    echo "Other"
else
    echo "No match"
fi
```

Case-insensitive compare trick:
```bash
${1,,}   # lowercase
${1^^}   # uppercase
```

## Case Statement
```bash
case "$1" in
  herbert|john)
    echo "Known user"
    ;;
  help)
    echo "Help selected"
    ;;
  *)
    echo "Unknown"
    ;;
esac
```

## Functions
variables are global by default. Use local variables by creating them inside functions

```bash
greet() {
  local name="user"
  echo "Hello $name"
}

greet
```

## Arrays
```bash
LIST=(one two three four)

echo ${LIST[0]}
echo ${LIST[@]}   # all elements
```

## For Loop
```bash
for item in ${LIST[@]}; do
  echo -n "$item "
done
```

## sed (Stream Editor)

```bash
# search and replace text using regex
sed 's/fly/grasshopper/g' test.txt
```

```bash
# format
s/old/new/g
```
`s` = substitute <br>
`g` = global (all matches)

## Here Document (EOF)
lets you pass **multi-line text** directly into a command from inside your script or terminal

```bash
# multi-line input
cat << EOF
line one
line two
EOF
```

## Word and Character Count
```bash
wc -w file.txt   # word count
wc -c file.txt   # character count
```
