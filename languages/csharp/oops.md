## Classes and Struct
`struct` &rarr; value type, saved on stack, no OOPS, and used for smaller stuff

`class` &rarr; reference type, saved on heap, OOPS, and used for complex stuff

```c#
class/struct Point {
    public int X;
    public int Y;
}

Point p1 = new Point{X=1, Y=2};
p1.X = 3
```

## Object Oriented Programming Basics (OOP)
`objects` &rarr; they are instances of classes

`classes` &rarr; blueprint for objects

`Fields` &rarr; raw storage for variables, no security

`Properties` &rarr; controlled access, only class can access values. needs a backing field (`_name`)

`virtual` &rarr; allows override

`override` &rarr; replaces behavior

`Access Modifier` &rarr; keywords

`Access Control` &rarr; design concept of controlling who can access (access modifiers, encapsulation, validation, properties, interfaces)

```c#
// field
public int Age;

// property
// automatic
public int Age {get; set;}

// manual logic - read everywhere, writable only in class
public int Age {get; private set;}

````

`Constructor` &rarr; special method called after initialization of a object

```c#
// constructor
class User {
    public User(int A){
        Name = A;
    }
}

// virtual and override
// virtual allows to override later
class Animal {
    public virtual void Speak() { ... }
}

// override will use this method for its objects
class Dog: Animal {
    public override void Speak() { ... }
}
```

`static` &rarr; cannot change value after compile time <br>
`static class` &rarr; not allowedto instantiate, only static members, no inheritance <br>
`static method` &rarr; belongs to class not instance, utility behavior, no instance is required <br>
`static fields` &rarr; shared with all instances <br>
`static constructors` &rarr; no access modifier, runs once per class (before first use)
```c#
class Config {
    public static string Mode;
    static Config() {
        Mode = "Production";
    }
}
Console.WriteLine(Config.Mode); // runs automatically
```

```c#
// sealed - no inheritance. it is complete
// class
sealed class Dog { ... }

// method
public sealed override void Speak() { ... } // cannot be changed

// unsealed is normal classed/methods
```

## Access Modifiers
`public` &rarr; accessible anywhere

`private` &rarr; only accessible inside the class

`protected` &rarr; accessible only in classes + subclasses

`internal` &rarr; accessible in same project/assembly

<table>
  <thead>
    <tr>
      <th>Encapsulation</th>
      <th>Inheritance</th>
      <th>Polymorphism</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Hides internal data</td>
      <td>Child reuses parent behavior</td>
      <td>Same base type, different behavior</td>
    </tr>
    <tr>
      <td>Only controlled access</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Nobody can affect data without going through your rules</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>

#### Examples
```c#
// encapsulation
class BankAcc {
    private string _num;
    public Deposit(string num){
        // below is a rule. only after going through rule does it save
        if(num > 10){
            _num = num
        }
    }
}

// inheritance
class Animal {
    public void Eat() { 
        ...
    }
}

class Dog: Animal {
    ...
}

// polymorphism
class Animal {
    public virtual void Speak() { 
        ...
    }
}

class Dog: Animal {
    public override void Speak() { 
        ...
    }
}
Animal a = new Dog()
a.Speak() // speak of Dog is called
```

## Abstract Class
they are incomplete classes, cannot be instantiated as they are

```c#
abstact class Shape {
    public abstract double Area();
}

class Circle: Shape {
    public override double Area() {
        return ...
    }
}
```

## Interface
- only contracts
- multiple interfaces can extend a single class
- no implementation. no access modifiers
- used for building loosely coupled apps

```c#
public interface ITax {
    int Calculate();
}

class Order: ITax, IMoney {
    public int Calculate() {
        ...
    }
}
```

<table>
  <thead>
    <tr>
      <th>Interface</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>No modifier field</td>
      <td>Multiple inhertance</td>
    </tr>
    <tr>
      <td>Can have fields</td>
      <td>Single Inheritance</td>
    </tr>
  </tbody>
</table>

## Namespaces
A **logical container** for types that holds classes, structs, interfaces, enums, etc...

- `logical` &rarr; grouped by meaning
- groups related code
- helps to organize large projects
  
```c#
namespace MyApp.Models;

// example structure of namespaces
// using MyApp.Data.Sql
MyApp
 ├─ Models
 │    └─ User.cs
 ├─ Services
 │    └─ ...
 └─ Data
      └─ Sql.cs
```

### 'using' Directives
- we can import namespaces with the keyword `using`
```c#
using System;
using System.Collections.Generic; // has List<int>
Console.WriteLine()

Generic.List<int> // if we import only System.Collections;
```

## Exception Handling
Exception creates a <u><b>Runtime Error Object</u></b> that is <u><b>thrown/shown</b></u>

Exception needs to be caught or else program will crash

```c#
// normal exception blocks
try {
    // risky code
} catch (Exception e) {
    // handle exceptions that are thrown
    Console.WriteLine(e.Message);
} finally {
    // always runs
}

// we can raise our own exception
if(age < 0) {
    throw new ArgumentException("Age cannot be negative");
}
```

#### Custom Exceptions
```c#
class SomeException: Exception {
    public SomeExeption(string msg) : base(msg) {}
}

// in code
throw new SomeException("Big Error!!!");
throw ex; // throw exception (resets stacktrace) (only in catch)
throw; // stops program (keeps stacktrace) (only in catch)
```
- Exceptions are expensive, better to use `TryParse`

## Generics
It has `Generic Classes` and `Generic Methods`

It is represented by `T` and can even be a custom class

A few examples are: `List<T>, Dictionary<TKey, TValue>, Task<T>, Nullable<T>`

It has automatic type inference

```c#
// generic methods
static void Print<T>(T value) {}
// where T: Animal or T: IDisposable and so on
```

## Delegates, Actions, Funcs, Events
`delegate` &rarr; interface for method. stores method. it is a **custom type**. stores references to a list of methods. anyone can control delegate. we can subscribe (+=) and unsubscribe (-=) to other methods

`Action\<T>` &rarr; ready made delegate returning void

`Func\<T, T>` &rarr; same as Action\<T> but has return type

`event` &rarr; something happens and it'll notify to subscribers. it is a delegate with restrictions. in events only outsiders can sub/unsub, only class cna trigger it, and it needs a type (delegate). it needs to have store and call methods (delgates)

```c#
// delegate example
public delegate void Notify(string message);
Notify n = SayHello;
n+=AnotherMethod
// n = [SayHello, ANotherMethod]
n("Hi") // runs all functions in List

// event example
public delegate void Notify(string message);
class Channel {
    public event Notify OnVideoUploaded;
    public void UploadVideo(string title) {
        OnVideoUploaded?.Invoke(title);
    }
}
```

## LINQs and Lambda Expression
`Lambda Expression` &rarr; x => x > 3
```c#
List<int> nums1 = new List<int> { 1, 2, 3, 4, 5, 6 };
List<int> nums2 = new List<int> { 4, 5, 6, 7, 8 };

List<string> words1 = new List<string> { "apple", "banana", "cherry", "date" };
List<string> words2 = new List<string> { "banana", "date", "fig", "grape" };

// filtering
var evens = nums1.Where(x => x % 2 == 0);
bool hasEven = nums1.Any(x => x % 2 == 0);
bool hasApple = words1.Contains("apple");

// transform
var squares = nums1.Select(x => x * x); // returns whatever the lambda expression returns
var upper = words1.Select(w => w.ToUpper());
var desc = nums1.OrderByDescending(x => x);
var sorted = nums1.OrderBy(x => x);
var sortedWords = words1.OrderBy(w => w.Length).ThenBy(w => w); // for ties

// aggregates
int count = nums1.Count(x => x > 3);
int sum = nums1.Sum();
double avg = nums1.Average();
int max = nums1.Max();
int min = nums1.Min();

// element operators
var first = nums1.First(x => x > 3);
var maybe = nums1.FirstOrDefault(x => x > 10); // 0
var single1 = nums1.Single(x => x == 3); // 3
// var single2 = nums1.Single(x => x == 10); // gives exception since no matches
// var single3 = nums1.Single(x => x > 2);   // gives exception since multiple matches
var singleOrDefault = nums1.SingleOrDefault(x => x == 10); // 0
// Console.WriteLine(first.GetType());
// Console.WriteLine(first);

// paging
var skip = nums1.Skip(2); // skips first 2
var take = nums1.Take(3); // returns first 3

// set operators
var distinct = new List<int> { 1, 1, 2, 2, 3 }.Distinct();
var union = nums1.Union(nums2);
var intersect = nums1.Intersect(nums2);
var except = nums1.Except(nums2);

// other
var concat = nums1.Concat(nums2);
```

## Nullables
normally only reference types are nullable

`null` &rarr; no value at all <br>
`""` &rarr; empty string <br>
`0` &rarr; integer value

`int?` &rarr; value types can become nullable

`!= null` &rarr; a null check

`??` &rarr; a null fallback. value to take if it is null

`?.` &rarr; return null if anything in chain is null

## Aync/Await
used for API calls, File reading, DB calls, and other non-blocking operations

**must return a `Task` or `Task<T>` or void**

`Task` &rarr; a promise of future data/return value
```c#
public async Task<int> getData() {
    await Task.Delay(1000);
    return 42;
}
int x = await getData() // wait until function is completed but can perform other operations

// others
var task = getData() // task is a Task (other data after this line can be run)
int x = await task; // return the value here
```

## Extension Methods and Dynamic
Extension Methods add methods to a class without modifying existing code.

static classes and methods only

```c#
public static class MyExtensions {
    // 'this string' adds this method to string class
    public static method void SayHi(this sting name) {
        Console.WriteLine("Hi" + name);
    }
}
string name = "Hussain";
name.sayHi();
```

Dynamic turns off compile time checking
```c#
dynamic x = "hello";
x.Something() // compiles but gives runtime error
```

## SOLID Principles
**S** &rarr; Single Responsibility (one entity)

**O** &rarr; Open/Closed System (add extension, but no modification)

**L** &rarr; Liskov's Substitution (sub-class has all properties of super-class)

**I** &rarr; Interface Seggregation (don't add useless Interface Methods for a Class)

**D** &rarr; Dependency Inversion (always use abstraction and not concrete implementation. high level does not depend on low level. so we have HL &rarr; Interface &rarr; LL)

other principles are ACID Transactions and Enterprise Pattern

## Dependency Injection
Dependencies &rarr; objects/components a class needs to function properly. they are necessary tools taht a class relies on to perform its task

Dependency Injection is a **Design Pattern** used to achieve Inversion of Code (helps follow SOLID)

A class doesn't create own dependencies, they are provided from outside

Constructor Injection &rarr; dependencies are provided through class constructor. receives all dependencies at object creation

Setter Injection &rarr; dependencies are assigned to public setter. receive all dependencies at object creation

Interface Injection &rarr; provided through Interface. a class has to implement the interface to receive dependency

```c#
// Builder depends on Hammer (without DI)
public class Hammer {
    public void Use() { ... }
}

public class Builder (
    private Hammer _hammer; // its a field and not a property
    public Builder() {
        _hammer = new Hammer() // Builder is responsible for creating his dependencies
    }

    public void BuildHouse() {
        _hammer.Use();
    }
)

// DI examples
// constructor
public Builder(Hammer hammer) {
    _hammer = hammer;
}

// setter
public class Builder (
    public Hammer hammer {get; set;}
)

Main(string args[]) {
    Hammer hammer = new Hammer();
    Builder builder = new Builder();
    builder.Hammer = hammer;
}
```

## Other
### Entities, Classes, Interfaces
`Entities` &rarr; it is something that has identity, exists as a distinct thing, is tracked separately from other objects

`Classes` &rarr; language contruct, that have methods and implementations

`Interfaces` &rarr; language construct, that only has method definitions

### Object Initializers
Classes can have multiple constructor overloads
```c#
var person = new Person {
    FirstName = "Hussain",
    LastName = "Kazarani"
};

<Parent Type> variable = new <Child Type>();
// new - runtime object

// creates a Dog variable
// can use all Dog methods
Dog d = new Dog();

// create a Dog object
// store in Animal variable
// only Animal methods are available
// only when Child inherits from this Parent
Animal a = new Dog();
```

### Indexers
```c#
var array = new int[5];
array[0] = 1; // 0 is an indexer
```

### Coupling
Measure of how interconnected classes and sub-systems are

Tightly vs Loosely Coupled

### Composition
Allows one to contain the other (has-a) `Eg: Car has-a Engine`

### Upcast/Downcast
When we have Parent and Child Classes, we need to convert a object into one or the other

```c#
// upcast (child to parent) (always safe)
Dog d = new Dog();
Animal a = d; // not a problem as a Dog is a Animal

// downcast (parent to child) (risky)
Animal a = new Dog();
Dog d = (Dog)a; //this will only world if it was Animal a = new Dog()
```

### is/as operator
```c#
// is - type checking
// if Parent is a Child
if(a is Dog) {
    Dog d = (Dog)a;
}

// as - safecasting that returns null
```

### Boxing/Unboxing
needed because some APIs can expect objects

```c#
// Boxing - value type is wrapped into object
int x = 5;
object o = x;

// Unboxing - object to value type
object o = 5;
int x = (int)o;
```

### Sealed/Unsealed
can be classes or methods

`Unsealed` - virtual &rarr; override &rarr; override &rarr; override

`Sealed` - virtual &rarr; override &rarr; STOP

### Records
in records, classes made for data and not behavior

in records, classes compare by value instead of reference

```c#
public record User(string Name, int Age);
var u1 = new User("A", 20);
var u2 = new User("A", 20);
u1==u2 // checks values and not reference
```

### Immutability
cannot change after creation

```c#
class User {
    public string Name {get;}

    public User(string name) {
        Name = name;
    }
}
```

### Composition > Inheritance
Composition is combining different parts instead of having a single Parent

`Inheritance` &rarr; gives Abstraction, Tightly coupled

`Composition` &rarr; lesser Abstraction, Loosely coupled, More boilerplate `Eg: Interface`

### Attributes
#### Metadata Tags on Code
```c#
[obsolete], [serializable]
void Something() {} // get the warnings above function from compiler
```

#### Reflection
```c#
// inspect code at runtime
var t = typeof(User);
var props = t.GetProperties();
```

#### IDisposable/IEnumerable
```c#
// IDisposable - cleaning resources
class Something: IDisposable {
    publicvoid DIspose() { ... }
}

// IEnumerable - type that can be iterated and returns as a object
foreach(var x in thing) { ... }
```

#### this
```c#
// this - current object instance OR speacial case (extension method)
// 'this' marks the type as being extended in extension method
public static class StringExtension {
    // 'this string' adds this method to string class
    public static bool IsLong(this sting s) {
        return s.Length > 10;
    }
}
string name = "Hussain";
Console.Writeline(name.IsLong());
```