## Project Structure
```
Solution Folder
 ├─ .sln
 ├─ Project1 Folder
 │    ├─ Program.cs
 │    ├─ .csproj   
 │    ├─ bin/
 │    └─ obj/
 └─ Project2 Folder
      ├─ Program.cs
      ├─ .csproj   
      ├─ bin/
      └─ obj/ 
```

`.sln` file &rarr; handle multiple projects

`Project` &rarr; can have multiple `Main()` functions. we can run each one via `Startup Object`

> there is a solution view (open by clicking `.sln` file) and also a file structure view

## .NET Platform
- .NET is a Platform that allows us to write Application that run on Windows, MacOS, and Linux
- There are 3 versions of `.NET` :
- `.NET Framework` is the old one (v4.8.1) and only works for Windows
- `.NET Core` is the new cross-platform version and was later rebranded to `.NET`
- `ASP.NET Core` is a Framework on `.NET` which is used for Web Applications.

<table>
    <tr>
        <th>Legacy</th>
        <th>1st Rewrite</th>
        <th>2nd Rewrite</th>
    </tr>
    <tr>
        <td>1.0 to 4.8.1</td>
        <td>.NET Framework</td>
        <td>ASP.NET</td>
    </tr>
    <tr>
        <td>1.0 to 3.1</td>
        <td>.NET Core</td>
        <td>ASP.NET Core</td>
    </tr>
    <tr>
        <td>5.0 to 10.0</td>
        <td>.NET</td>
        <td>ASP.NET Core</td>
    </tr>
</table>

```
                C# History
2002 ────●── .NET Framework 1.0 (Foundation)
         │
2005 ────●── .NET Framework 2.0 (Generics)
         │
2007 ────●── .NET Framework 3.5 (LINQ)
         │
2012 ────●── .NET Framework 4.5 (async/await)
         │
2016 ────●── .NET Core 1.0 (Cross-platform)
         │
2019 ────●── .NET Core 3.1 LTS
         │
2020 ────●── .NET 5.0 (Unification)
         │
2021 ────●── .NET 6.0 LTS (Minimal APIs, MAUI)
         │
2022 ────●── .NET 7.0 (Performance focus)
         │
2023 ────●── .NET 8.0 LTS (Native AOT, Blazor upgrades)
         │
2024 ────●── .NET 9.0 (Latest STS)
         │
2025 ────●── .NET 10.0 LTS (Next LTS wave)
```

### Introduction
- `.NET` is a Platform that consists of Libraries, Tools, Compilers, CLI, Runtime, SDK, etc to create applications
- It's written in PascalCase
- `CLR (Common Language Runtime)` &rarr; it is the execution engine that runs `.NET` applications. its cus different OS have different architecture. it handles the following:
  - JIT
  - Memory Management
  - Type Safety
  - Exception Handling

> <b>C# &rarr; Compiled &rarr; Interpreted Representation &rarr; CLR &rarr; Machine Code &rarr; Runs</b> <br>
> Execution Code: <b>App &rarr; Assembly &rarr; Namespace &rarr; Class &rarr; Data & Methods</b>

## Create Project
```c#
dotnet new console -n HelloApp
dotnet new console --use-program-main -n HelloApp
dotnet build
dotnet run

Program.cs // the main C# file
HelloApp.csproj // has dependencies, versions, config, packages
bin/ // compiled stuff
obj/ // cached stuff, system dependencies, intermediate files, helps in rebuild
.NET // platform
ASP.NET // forces structure so it is a framework
```

```c#
// Main entrypoint
using System;
class Program{
    static void Main(string args[]){
        Console.WriteLine("Hello");
    }
}
```

## Syntax
```c#
int, double, float(1.5f), decimal(1234.432m)
bool = true or false
string, char
var name = "Hussain" // we must assign value immediately
var userList = new List<string>() // we can specify type
const // cannot change value after compiler runs (aka assign value immediately)
+, -, *, /, % // operators
10/3 // output: 3 (int division)
10.0/3 // output: 3.33 (double division)
x++, x--
==, !=, >, <, >=, <= // comparison operators
$$, ||, ! // logical operators


// strings
char var1 = 'A';
string var2 = "Hello";
Console.Write($"{var2} Hussain!");
```
### Typing
`Explicit Typing` &rarr; specify type (List<string>())

`Implicit Typing` &rarr; compiler infers (var a=2)

`Generic Type` &rarr; can be any type (List<T>)

### Control Flows
```c#
// if statement
if(){
    ...
} else if(){
    ...
} else {
    ...
}

// loops
for(i=0; i<5; i++) { ... }
while() { ... }
do { ... } while ( )
foreach(var name in names) { ... }

// switches
int day = 3;
switch(day) {
    case 1:
        Console.Write()
        break;
    case 2:
        Console.Write()
        break;
    default:
        Console.Write()
        break;
}

break, continue
```

### Methods/Functions
```c#
// function
returnType Name(parameters) { ... }

// optional parameters. always keep it last
static void Welcome(string name="Guest") { ... }

// why last?
static void Bad(int x=5; int y) { ... }
Bad(10) // where's why?
```

### Method Overloading
same method name, different parameter signatures
```c#
static void Add(int x, int y) { ... }
static void Add(double x, double y) { ... }

Add(1, 2);
Add(10.1, 20.2);
```

### Parameter Modifiers (ref, out, in)
```c#
// C# is Pass by Value

// ref - change orignal value
// must be initialized
static void AddTen(ref int number) {
    number+=10
}

int n = 5;
AddTen(5);
Console.WriteLine(n); // output: 15

// out - method assigns value
// must assign before method ends
static void Divide(int n, int b, out int result) {
    result = a/b;
}

Divide(10, 2, out int r);
Console.WriteLine(r); // output: 5

// in - pass reference but read only
static void Show(in int x) {
    Console.WiteLine(x);
    x = 10; // ❌ ILLEGAL
}

int n = 7;
Show(in n);
```

## `static` Context
`static` &rarr; if given to a function inside a class, it is tied to the class instead of the object/instance
```c#
MathUtil.Add(1, 2); // called via class name
```
### Why is `Main()` static?
this is because it needs to run without creating an object of itself (which will become an infinite loop)

static methods can call only other static methods. it can be used to call classes and methods but we would need to create instances.

## Value Types and Reference Types
<table>
    <tr>
        <th>Value Types (copy)</th>
        <th>Reference Types (reference)</th>
    </tr>
    <tr>
        <td>int</td>
        <td>class</td>
    </tr>
    <tr>
        <td>double</td>
        <td>string</td>
    </tr>
    <tr>
        <td>bool</td>
        <td>array</td>
    </tr>
    <tr>
        <td>char</td>
        <td>object</td>
    </tr>
    <tr>
        <td>struct</td>
        <td>List<T></td>
    </tr>
    <tr>
        <td>decimal</td>
        <td>Dictionary< k,v ></td>
    </tr>
    <tr>
        <td>DateTime</td>
        <td></td>
    </tr>
</table>

## Strings
> they are immutable <br>
> they are `reference type`, but on modification act like `value type` <br>
> creates new string object pointing to variable on changing value <br>
> cannot mutate same string (s[0] = `H` ❌)

```c#
sentence.Substring(0, n); // give first `n` characters
sentence.Split(" "); // spilt by spaces. gives back List<string>
var sum = String.Join(" ", summaryWords) + "..."; // add a space between all the words
sentence.Replace("Hello", "Bye"); // replace ` sHello` with `Bye`
```

<u><b>string[] vs List<string></b></u> <br>
`string[]` &rarr; fixed sized array <br>
`List<string>` &rarr; generic list

```c#
// string[]
string[] names = new string[3];
names[0] = "Ana";
names[1] = "Bob";

// list<string>
List<string> names = new List<string>();
names.Add("Ana");
names.Add("Bob");

// length methods
list.Count;
arr.Length;

string[] arr = list.ToArray();
List<string> list2 = arr.ToList();
```

## Collections
1. <u><b>Arrays</b></u> &rarr; fixed size
    ```c#
    int[] numbers = new int[3];
    int[] numbers = {10, 20, 30};
    numbers[0] = 10;
    numbers.Length;
    ```

2. <u><b>List\<T></b></u> &rarr; dynamic array
    ```c#
    List<int> list = new List<int>();
    var list = new List<int>{1, 2, 3};
    list.Add(10);
    list[0]
    list.Count
    list.Remove(value), list.RemoveAt(index)
    ```

3. <u><b>Dictionary\<TKey, TValue></b></u> &rarr; key-value mapping
    ```c#
    Dictionary<string, int> dict = new Dictionary<string, int>();
    dict["apple"] = 5 OR dict.Add("apple", 5)
    dict["apple"] // read value
    dict.TryGetValue("pear", out int value)
    dict.ContainsKey("apple")

    foreach(var pair in dict) {
        pair.Key, pair.Value
    }
    ```

4. <u><b>HashSet\<T></b></u> &rarr; unique items only, no index access

5. <u><b>Queue\<T></b></u> (FIFO) &rarr; `q.Enqueue()`, BFS, buffers

6. <u><b>Stack\<T></b></u> (LIFO) &rarr; `s.Push()`, DFS

7. <u><b>IEnumerable\<T></b></u> &rarr; a type which can be looped over

## TryVars
```c#
// bad input
string text = "Hello";
int age = int.parse(text); // crashes program

// conditionals
if(int.TryParse(text, out int age)) { ... } 

// TryVars
int.TryParse(text, out int age)
dict.TryGetValue("pear", out int value)
```

## Console
```c#
Console.WriteLine($"Hello {variable}")
Console.Write() // no new line
Console.ReadLine() // returns string

string? name = Console.ReadLine() // can be NULL
```

## Overflow
```c#
int x = int.MaxValue
x = x + 1; // wraps around by default
// an explicit check that allows it to wrap to lowest value
checked {
    int x = int.MaxValue
    x++;
}
```

## Scope
- we have `Block`, `Loop`, and `Method` scope
- no global scope, only `static` fields

## Type Conversion/Casting
<u><b>Conversion</b></u> &rarr; change the type of a value <br>
<u><b>Casting</b></u> &rarr; syntax to force a conversion (one way of explicit conversion)

```c#
// implicit conversion
int a = 10;
double b = a;

// explicit conversion
double x = 9.8;
int y = (int)x;
int n = int.Parse("123");
```

## DateTime and TimeSpan
`DateTime` &rarr; date and time <br>
`TimeSpan` &rarr; length of time/difference between 2 DateTime's

```c#
// DateTime
DateTime now = DateTime.Now;
DateTime utc = DateTime.Utcnow;
var d = new DateTime(yyyy, MM, dd);
var time = DateTime.Now.AddDays(3).AddHourse(1);

// TimeSpan
var timespan = new TimeSpan(H,M,D);
TimeSpan.FromHours(1);

timespan.<property>
TotalHours, TotalSeconds, TotalMinutes
Days, Hours, Minutes, Seconds
Add, Subtract // example: timespan.Add(TimeSpan.FromMinutes(8))

// parsing
now.ToString("yyyy-MM-dd HH:mm") // custom date format
TimeSpan.parse("01:02:2004")
```

## StringBuilder
strings are Immutable so changes create many new objects

StringBuilder creates a <u><b>mutable string buffer</b></u>

```c#
using System.Text

var sb = new StringBuilder();
for(int i=0; i<1000; i++) {
    sb.Append(i);
}

// auto-casts like 10.0/3, only first type is considered
sb.Append("Hello");
sb.AppendLine("World")
sb.Insert(0, "Start ");
sb.Replace("World", "C#");

// same but inefficient way, new object created everytime
string s = "";
for(int i=0; i<1000; i++) {
    s+=i
}
```

## Other
### Enums
`enums` &rarr; a named set of constant values <br>
can cast `enum to int` and `int to enum`

```c#
enum Status {
    Pending = 1
    Approved = 5
    Rejected = 9
}

Status s = Status.Pending

// casting
int n = (int)s
status s2 = (status)n
```

### File I/O
consists of:

`static` &rarr; File, Directory

`instance` &rarr; FileInfor, DirectoryInfo

`other` &rarr; Path

```c#
using System.IO

// files
// write
File.WriteAllText("data.txt", "Hello") // overwrite
File.AppendAllText("data.txt", "\nMore") // append

// read
string content = File.ReadAllText("data.txt") // whole file
string[] lines = File.ReadAllLines("data.txt") // all in lines

File.Exists("data.txt")
Create(), Copy(), Delete(), More(), GetAttributes()

// folder
CreateDirectory(), Delete(), Exists(), GetCurrentDirectory()

// paths
var path = @"c:\temp\something.jpg" // write down a path
var fileInfo = new FileInfo(path)
Path.GetExtension(path)
Path.GetFileName(path)
Path.GetFileNameWithoutExtension(path)
Path.GetDirectoryName(path)

GetFiles(), Move(), GetLogicalDrives()
```

### Debug Mode
```bash
F9 - Breakpoints
F10 - Step Over
F11 - Step Into

Windows -> Debug -> Call Stack
Debug -> Windows -> Autos/Locals # variables in scopes
Defensive Programming
```

### JSON Serialize/Deserialize
`Serialize` &rarr; object to JSON string <br>
`Deserialize` &rarr; JSON to object <br>
JSON works with only public properties

```c#
using System.Text.Json;

class User {
    public string Name { get; set; }
    public int Age { get; set; }
}

User u = new User
{
    Name = "Hussain",
    Age = 21
};

string json = JsonSerializer.Serialize(user); // change object to json
User u2 = Json.Serializer.Deserialize<User>(json); // change json to object
```

### Random
```c#
var rng = new Random() // new object

// upper bound
int n = rng.Next(10) // 0-9 (exclusive)

// min and max range
int n = rng.Next(5, 11) // 5-10

// doubles
double x = rng.NextDouble(); // 0.0 <= 1.0

// scale
double price = rng.NextDouble() * 100; // 0-100

// bool
bool b = rng.Next(2) == 0;

// random items
var items = new List<string>{"A", "B", "C"};
var pick = items[rng.Next(items.Count)];

// `Crypto`is a module that is the safer, but slower way of Random
```

### Typing
```c#
x.GetType()
typeof(string)

if(x.GetType() == typeof(string)) { ... }
```

## Field and Property
`Field` &rarr; variable inside class

`Property` &rarr; uses a method behind-the-scenes to get value. it generates private methods like `getName` and `setName`

## Getter/Setter
used to create `Rules` which is what someone accessing has to go through. basically makes the call more secure <br>
each class variable has own rules <br>

`Setter` &rarr; has a special value keyword (_name = value)

`Getter` &rarr; only gets `_name`

```c#
class User {
    public string Name{ get; set; } // creates private methods through which value is accessed after passing rule
}

// custom names
class User {
    private string _name;
    public string Name {
        get => _name;
        set {
            Console.WriteLine();
            _name = value; // special keyword to store incoming store
        }
    } 
}
```
