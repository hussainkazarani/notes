## Basics
`...` &rarr; for pass

```python
# strings
text = 'hello'
text = "Hello"
text = `hello` ❌ # no backtick option in python
type(text) # type in python is 'str'
# f-strings
print(f'Hello {variable}')
```

## Environment
```python
python -m venv <name> # convention is .venv
source .venv/bin/activate
pip install <package_name>
pip freeze > requirements.txt
pip install -r requirements.txt
```

## Concepts
### \_\_name\_\_ in Python File
```python
# example.py
if __name__ == "__main__":
    print("Stuff")
```
`__name__` &rarr; Dunder Name

`__main__` &rarr; Dunder Main

- only runs the code  inside the `Dunder Main` if the file is run `python example.py` instead of being imported as a package.

- every file inside python is a package

### __init\__.py
- used in older versions of python
- to define a folder as a package
- in newer versions, usually used for following conventions and easier imports

```python
entire-app/
├─ main.py # import utils
└─ utils/
    ├─ math_utils.py
    └─ __init__.py # from .math_utils.py import add
```

### Imports
- `math_utils` &rarr; checks the executed file directory
- `.math_utils` &rarr; checks this files directory
- `..math_utils` &rarr; checks the parent of this file directory

### \_\_init\_\_ Method
```python
class Rect:
    def __init__(self,x,y): # refers to how to initialize this particular(self) new object
        self.x = x
        self.y = y

Rect(2,3)
```

- everything in python is an object/instnace
- you can check with the following code:
```python
print(type(func))
```
- every operation `[+, len()]` are done by/mapped to dunder methods `[__add__(), __len__()]`

### List Comprehension
```python
print([name for name in person if len(name) > 7]) # first name is the variable its stored in everytime
```

### Python OOPS
- class is a blueprint to create objects
- `__init__` methods of classes help give data to objects \***on initialize**\*

```python
# Example-1
class Microwave:
    ...

# calls
# `:Microwave` -> it give specific typing with type annotation
# `Microvewave()` -> creates empty object/instance of class 
smeg:Microwave = Microwave() 


# Example-2
# `self` -> used to refer to a specific instance of object
# `None` -> its the return type. not always necessary
class Microwave:
    def __init__(self, brand:str, power_rating:str) -> None:
        self.brand = brand
        self.power_rating = power_rating

# calls
smeg:Microwave = Microwave('Smeg', 'B')
print(smeg)
print(smeg.brand)
```

- all functions in a class need `self` and `return type`
```python
def run(self) -> None:
```
- can also perform operations like add(+) to instances using dunder methods
- `repr` and `str` Dunders are also used
```python
def __add__(self,other):
    print(self.brand + other.brand)
```
