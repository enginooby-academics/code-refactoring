# Python

### Declaration, Initialization & Assignment
+ Swap two variables using **tuple**
```py
# 👎 longhand
temp = a
a = b
b = temp

# 👍 shorthand
a, b = b, a
```


### Expressions
+ **Comparison chaining**
```py
# 👎 longhand
if a > 1 and a < 9

# 👍 shorthand
if 1 < a < 9
```

+ Check multiple flags w/ same value
```py
# 👎 longhand
if a == 1 or b == 1 or c == 1:

# 👍 shorthand
if 1 in (a, b, c):
```

+ Check multiple flags for truthiness/falsiness
```py
if a or b or c:

if(any(a, b, c)):
```

### Function
+ Return multiple values using **tuple**
```py
def test():
    return 'abc', 100
```

+ Use **```lambda```** for single statement functions
```py
# 👎 longhand
def subtract(x, y): 
    return x - y

# 👍 shorthand
subtract = lambda x, y : x - y
```

+ Use **```@cache```** decorator from **functools** library to cache expensive computations, esp. in recursive functions [[Python3.2](https://docs.python.org/3/library/functools.html#functools.cache)]
> Reason: improve performance
```py
# 👎 non-compliant
factorial = lambda n : n * factorial(n-1) if n else 1

# 👍 preference
@cache
factorial = lambda n : n * factorial(n-1) if n else 1
```



### String
+ Reverse string using **extended slices syntax**
```py
print("xyz"[::-1]) #zyx
```



### Collection
+ **Extended slices syntax**
 
To extract elements: ```range(10)[::2] #[0, 2, 4, 6, 8]```   
To reverse: ```range(10)[::-1] #[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]```

+ Use **list comprehension** to generate lists processed (w/ conditions or computations) from raw list:
```py
# 👎 non-compliant
odd_square = [] 
for x in range(1, 11): 
    if x % 2 == 1: 
        odd_square.append(x**2)
        
# 👍 preference
odd_square = [x ** 2 for x in range(1, 11) if x % 2 == 1] 
```

+ Use **unpacking generalizations** to merge dictionaties, overwrite duplicate [[Python3.5]](https://www.python.org/dev/peps/pep-0448/)
```py
# 👉 given
x = {'a': 1, 'b': 2}
y = {'b': 3, 'c': 4}

# 👍 preference
print({**x, **y}) #{'a': 1, 'b': 3, c': 4}
```



### OOP
+ Use **```@dataclass```** decorator from **dataclasses** library to generate common function implementations for classes such as ```__init__, __repr__, __eq__``` [[Python3.7](https://realpython.com/python-data-classes/)]
