# Python

### Declaration, Initialization & Assignment
+ Swap two variables using **tuple**
```
temp = a
a = b
b = temp

// shorthand
a, b = b, a
```


### Expressions
+ **Comparison chaining**
```
if a > 1 and a < 9
# shorthand
if 1 < a < 9
```


### Function
+ Return multiple values using **tuple**
```
def test():
    return 'abc', 100
```



### String
+ Reverse string using **extended slices syntax**
```
a = "xyz"
print(a[::-1]) #zyx
```



### Collection
+ **Extended slices syntax**
 
To extract elements: ```range(10)[::2] #[0, 2, 4, 6, 8]```   
To reverse: ```range(10)[::-1] #[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]```

