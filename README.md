> Alternative ways of writing code to help improving **code readability, clarity, brevity & performance**  

<a name="0"></a>  
# Table of Contents
+ Language-specific
+ Declaration, initialization & assignment
+ Control flow
+ Expressions
+ OOP
+ Function
+ String

### Language-Specific
|[C#](CS.md)|[C# in Unity](CS_UNITY.md)|[C++](CPP.md)|[C++ in Unreal Engine](CPP_UE.md)|[Java](JAVA.md)|[Dart](DART.md)|[Python](PYTHON.md)|[R](R.md)|[JS/TS](TS_JS.md)|[Go](GO.md)|
|---|---|---|---|---|---|---|---|---|---|

### Declaration, Initialization & Assignment
+ ~~Type annotation (explicit type)~~ => **type inference** (implicit type) for initializer expression and local variable _[C++11 ```auto```, C# ```var```, TS ```let```, Dart ```var```]_
> Pros: shorthand especially for long type init, focus more attention on local variable name and value

Initializer expression:
```csharp
// 👎 longhand
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();

// 👍 shorthand
var instance = new AReallyReallyLooooongClass();
```

For local variable:
``` csharp
// 👉 given
List<User> users = {User1, User2...};

// 👎 non-compliant
foreach(User user in users)

// 👍 preference
foreach(var user in users)
```

+ Assign w/ nullable variable 
```ts
// 👎 longhand
const result = (nullableVar !== null && nullableVar !== undefined) ? nullableVar : fallbackVar
```

Using **nullish coalescing operator ```??```** *[C#, PHP, ES11]*
```ts
// 👍 shorthand
const result = nullableVar ?? fallbackVar
```

Using **short circuit evaluation ```&&, ||```**
```ts
// 👍 shorthand
const result = nullableVar || fallbackVar
```

+ Assign default value for nullable variable using **logical nullish assigment operator ```??=```** *[TS/JS, C#8]*
```ts
// 👎 longhand
nullableVar = (nullableVar !== null && nullableVar !== undefined) ? nullableVar : defaultVal

// 👎 longhand
nullableVar ?? (nullableVar = defaultVal)

// 👍 shorthand
nullableVar ??= defaultVal
```

+ **Multiple variable declaration** for related variables _[JS/TS, C#, Java, Go]_
```ts
// 👎 longhand
let a;
let b;
let c = 3;

// 👍 shorthand
let a, b, c = 3;
```

+ Assign multiple variables using **object destructuring/tuple** _[ES6, C#, Python]_
```ts
// 👎 longhand
let a = 1;
let b = 2;
let c = 3;

// 👍 shorthand
[a, b, c] = [1, 2, 3]
```

+ Swap two variables using **XOR ```^```**
> ✔️ Pros: avoid using third temporary variable  
> ❌ Cons: purpose may not seem straightforward 
```csharp
// 👎 longhand
temp = a;
a = b;
b = temp;

// 👍 shorthand
a ^= b ^= a ^= b;
```
  
### Control Flow
+ **Guard clause/assert/precondition**: early return for special case; multiple return statements
> ✔️ Pros: avoid nested statements, improve readability  
> ⚠️ Cautions: too many return statements (esp. void) will make code unobvious and harder to debug
```ts
// 👎 non-compliant
function getInsuranceDeductible(insurance){
  if (insurance.covered) {
    if (insurance.majorRepair) {
      return 500
    } else if (insurance.mediumRepair){
      return 300
    } else {
      return 100
    }
  } else {
    return 0
  }
}

// 👍 preference (use daisy chaining ternary operator to shorten furthermore)
function getInsuranceDeductible(insurance){
  if (!insurance.covered) return 0
  if (insurance.majorRepair) return 500
  if (insurance.mediumRepair) return 300

  return 100
}
```

+ **Ternary operator ```? :```**

To assign value:
```ts
// 👎 longhand
if (a > b) {
    result = x;
}
else {
    result = y;
}

// 👍 shorthand
result = a > b ? x : y;
```

To return:
```ts
// 👎 longhand
if (a > b) {
    return x;
}
else {
    return y;
}

// 👍 shorthand
return a > b ? x : y;
```

To shorten switch w/ multiple return statements using **daisy chaining**:
```ts
// 👎 longhand
function getInsuranceDeductible(insurance) {
  if (!insurance.covered) return 0
  if (insurance.majorRepair) return 500
  if (insurance.mediumRepair) return 300

  return 100
}

// 👍 shorthand
function getInsuranceDeductible(insurance) {
  return insurance.covered ? 0
         : insurance.majorRepair ? 500
         : insurance.mediumRepair ? 300 
         : 100
}
```

+ Conditional w/ **falsy/truthy values** *[TS/JS, Groovy, Perl, PHP, Python, Ruby, C++ ```0, false```]*
```ts
// 👎 longhand
if(typeof a !== "undefined" && typeof b !== "null" && typeof c !== "NaN" && d !== "" && array.length !== 0)

// 👍 shorthand
if(a && b && c && d && array.length)
```
+ One-statement in conditional w/ **short circuit evaluation ```&&, ||```**
```ts
// 👎 longhand
if(isHungry && isSleepy) {
  code()
}

// 👍 shorthand
isHungry && isSleepy && code()
```



### Expressions
+ ~~Equality operator ```==```~~ => **Strict equality operator ```===```** *[TS]*

+ **Spaceship/three-way comparison operator ```<=>```** *[C++, Groovy, Kotlin, Perl, PHP, Ruby]*
```php
// 👉 given
$users = ['branko', 'ivana', 'luka', 'ivano'];

// 👎 longhand
usort($users, function ($a, $b) {
  return ($a < $b) ? -1 : (($a > $b) ? 1 : 0);
});

// 👍 shorthand
usort($users, function ($a, $b) {
  return $a <=> $b;
});
```


  
### OOP
+ **Constructor shorthand** *[TS, PHP8 (property promotion), Dart]*
```ts
// 👎 longhand
class User {
  private name: string;
  private age: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

// 👍 shorthand
class User {
  constructor(
    private name: string,
    private age: number
  ) {}
}
```

+ Explicitly declare access modifiers for class members
> Reason: clarify purpose of the member
```ts
class User {
  // 👎 non-compliant
  name: string;
  
  // 👍 preference
  public name: string;
}
```


### Function
+ Use **lambda expression/arrow function ```=>```** to declare single statement functions _[Java8, JS/TS (fat arrow), Dart, C# (expression-bodied members), Python ```lambda```]_
> Pros: bind _this_ to the invoker
```ts
// 👎 longhand
function getSum(a: number, b: number) {
  return a + b
}

// 👍 shorthand
const getSum = (a: number, b: number) => (a + b)
```

+ Pass a single-use callback function as an argument w/ **anonymous function**
> Pros: no need to declare a separate disposable function -> reduce coding overheating, often used along w/ collection operation such as map(), where(), and reduce(), etc


+ **Named argument** *[PHP8, Kotlin, C#, Python (keyword argument)]*
> Reason: for clarity, order of params could be changed, convenient to leave default arguments
```csharp
// 👉 given
public void doSomething(string foo, int bar) {...}

// 👎 non-compliant
doSomething("someString", 1);

// 👍 preference
doSomething(foo: "someString", bar: 1);
```

+ ~~Overloading functions~~ that differ only in trailing parameters => **optional parameters**
```ts
// 👎 non-compliant
interface Example {
  diff(one: string): number;
  diff(one: string, two: string): number;
  diff(one: string, two: string, three: boolean): number;
}

// 👍 preference
interface Example {
  diff(one: string, two?: string, three?: boolean): number;
}
```

+ ~~Promise/callback chaining~~ => **```async-await```** *[ES6, C#, Dart]*


### String
+ ~~```String```~~ => **```StringBuffer```** for string manipulations *[Java, C#]*
> Reason: do not create new String instances on manipulations -> save memory

+ ~~String concatenation operator ```+```~~ => **String interpolation/template literals ``` `${}` ```** *[ES, C#, Kotlin, PHP]*
```ts
// 👎 non-compliant
console.log("Sum of " + a + " and " + b + " is " + (a + b))

// 👍 preference
console.log(`Sum of ${a} and ${b} is ${a + b}`)
```

