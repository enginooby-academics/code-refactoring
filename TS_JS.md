# TypeScript & JavaScript

### Mathematics
+ **Exponent power**
```
const power = Math.pow(4, 3);
// shorthand 
const power = 4**3;
```
+ **Floor rounding**
```
const floor = Math.floor(6.8);
// shorthand 
const floor = ~~6.8;
```
+ **Decimal base exponents**
```
10000000
// shorthand
1e7
```

### Collection
+ **Spread operator (...)** [ES6]

For joining arrays:
```
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);
// shorthand
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
```
  
For cloning array:
```
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()
// shorthand
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```
