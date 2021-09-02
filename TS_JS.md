# TypeScript & JavaScript

### Declaration, Initialization & Assignment
+ ~~Explicit type (type annotation)~~ => **implicit type (type inference)**
```
const message: string = 'hello world'
//preference
const message = 'hello world'
```

### String
+ String to number *[ES]*
```
const num1 = parseInt("100");
const num2 =  parseFloat("100.01");
// shorthand
const num1 = +"100";
const num2 =  +"100.01";
```

### Number
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



### Module
+ **Barrel**
```
// user/WindowsUser.ts
export class WindowsUser {}

// user/LinuxUser.ts
export class LinuxUser {}

// user/AndroidUser.ts
export class AndroidUser {}
```
Import w/o a barrel:
```
import { WindowsUser } from '../user/WindowsUser';
import { LinuxUser } from '../user/LinuxUser';
import { AndroidUser } from '../user/AndroidUser';
```
Preference: create a barrel
```
// user/index.ts
export * from './WindowsUser';
export * from './LinuxUser';
export * from './AndroidUser';
```
Import from barrel:
```
import { WindowsUser, LinuxUser, AndroidUser } from '../user'; // user/index.ts is implied
```

+ ~~Default export~~ => simple export
> Pro: import name will update if rename the export entity
```
export default User
import User from './user'

//preference
export class User {}
import { User } from './user'
```
