# Python

### Declaration, Initialization & Assignment
+ Swap two variables using **tuple**
```py
temp = a
a = b
b = temp

// shorthand
a, b = b, a
```


### Expressions
+ **Comparison chaining**
```py
if a > 1 and a < 9
# shorthand
if 1 < a < 9
```


### Function
+ Return multiple values using **tuple**
```py
def test():
    return 'abc', 100
```
+ Prefer **lambda** for one-statement functions
```
def subtract(x, y): 
    return x - y
# shorthand
subtract = lambda x, y : x - y
```


### String
+ Reverse string using **extended slices syntax**
```py
a = "xyz"
print(a[::-1]) #zyx
```



### Collection
+ **Extended slices syntax**
 
To extract elements: ```range(10)[::2] #[0, 2, 4, 6, 8]```   
To reverse: ```range(10)[::-1] #[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]```

+ Use **list comprehension** to generate lists processed (w/ conditions or computations) from raw list:
```py
odd_square = [] 
for x in range(1, 11): 
    if x % 2 == 1: 
        odd_square.append(x**2)
        
# preference
odd_square = [x ** 2 for x in range(1, 11) if x % 2 == 1] 
```

+ Use **unpacking generalizations** to merge dictionaties, overwrite duplicate [Python3.5]
```py
x = {'a': 1, 'b': 2}
y = {'b': 3, 'c': 4}

print({**x, **y}) # {'c': 4, 'a': 1, 'b': 3}
```
