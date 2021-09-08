# TypeScript & JavaScript

### Declaration, Initialization & Assignment
+ ~~Explicit type (type annotation)~~ => **implicit type (type inference)**
```ts
// 👎 non-compliant
const message: string = 'hello world'

// 👍 preference
const message = 'hello world'
```



### Function
+ Use the return type **```void```** for callbacks whose value will be ignored
> Reason: prevents accidentally using the return value in an unchecked way
```ts
// 👎 non-compliant
function fn(x: () => any) {
  x();
}

// 👍 preference
function fn(x: () => void) {
  x();
}
```

+ Define a **type alias** to encapsulate callback type [TS]
```ts
// 👉 given
var numCallback = (result: number) : void => {alert(result.toString())};

// 👎 non-compliant
class User {
  save(callback: (n: number) => void) : void {
    callback(42);
  }
}

// 👍 preference
type NumberCallback = (n: number) => void;

class User {
  save(callback: NumberCallback) : void {
    callback(42);
  }
}
```




### Type
+ **Object property value shorthand** [ES6]
```ts
// 👉 given
let name = 'User 1';
let age = 18;

// 👎 longhand
var user = {
  name: name,
  age: age,
}

// 👍 shorthand
let user = {name, age}
```

+ ~~Enum~~ => **Union types** [[Reference](https://fettblog.eu/tidy-typescript-avoid-enums/?fbclid=IwAR18SiWtUFai4gEY4B6rm2nSGYfR54Yw3bitrkl4Ph9z72qwM_8kbOUYhX8)) *[TS]*]




### String
+ String to number [ES]
```ts
// 👎 longhand
const num1 = parseInt("100");
const num2 =  parseFloat("100.01");

// 👍 shorthand
const num1 = +"100";
const num2 =  +"100.01";
```



### Number
+ **Exponent power**
```ts
// 👎 longhand
const power = Math.pow(4, 3);

// 👍 shorthand
const power = 4**3;
```

+ **Floor rounding**
```ts
// 👎 longhand
const floor = Math.floor(6.8);

// 👍 shorthand
const floor = ~~6.8;
```

+ **Decimal base exponents**
```ts
// 👎 longhand
10000000

// 👍 shorthand
1e7
```



### Collection
+ **Spread operator ```...```** [ES6]

To join arrays:
```ts
// 👎 longhand
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);

// 👍 shorthand
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
```
  
To clone array:
```ts
// 👎 longhand
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()

// 👍 shorthand
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```



### Module
+ **Barrel**
```ts
// 👉 given
// 📄 user/WindowsUser.ts
export class WindowsUser {}

// 📄 user/LinuxUser.ts
export class LinuxUser {}

// 📄 user/AndroidUser.ts
export class AndroidUser {}
```

Import w/o a barrel:
```ts
// 👎 non-compliant
// 📄 app.ts
import { WindowsUser } from 'user/WindowsUser';
import { LinuxUser } from 'user/LinuxUser';
import { AndroidUser } from 'user/AndroidUser';
```

Import w/ a barrel:
```ts
// 👍 preference
// 📄 user/index.ts
export * from './WindowsUser';
export * from './LinuxUser';
export * from './AndroidUser';

// 📄 app.ts
import { WindowsUser, LinuxUser, AndroidUser } from 'user'; // user/index.ts is implied
```

+ ~~Default export~~ => simple export
> Pro: import name will update if rename the export entity
```ts
// 👎 non-compliant
export default User
import User from './user'

// 👍 preference
export class User {}
import { User } from './user'
```
