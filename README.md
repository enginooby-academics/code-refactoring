<a name="0"></a>  
# Table of Contents
1. [Abbreviations](#abbreviations)
2. [Naming](#naming) 
    + Variable & constant
    + Type & function
    + Git
3. [Commenting](#commenting)
    + Document
    + Task
    + Section
4. [Architecture](#architecture)
    + SASS/Less
    + NodeJS & TypeScript
5. [Refactoring](#refactoring)

<a name="abbreviations"></a>  
### I - Abbreviations
> Should be **universally accepted**, provide **good result of shortening**, used for naming & commenting
* **addr** address - **app** application
* **bg** background - **btn** button
* **char** character - **col** column - **coord** coordinate
* **db** database - **dest** destination - **dir** directory
* **len** length
* **msg** message
* **num** number
* **obj** object
* **pwd** password - **param** parameter - **pic** picture - **pos** position
* **str** string - **src** source
* **val** value - **var** variable

<a name="naming"></a>  
# II - Naming
[⬆ To the top](#0)
> Normally use camelCase for variables & functions/methods, SNAKE_CASE for constants, PascalCase for types, w/ prefix if necessary

### 1 - Variable & Constant
+ **Element/HTMLElement** ```e prefix```: *eBtn*
+ **NodeListOf\<Element>** ```es prefix```: *esBtn* (questionable?)
+ **JQuery\<HTMLElement>** ```$ prefix```: *$btn* (questionable?)
+ **Boolean** ```{is/have/can/do}+{noun}+{adj/verb-ed}```: *wasBtnClicked*, *areBtnsGreen*
+ **Private class member** ```_ prefix```: *_id* (questionable?)
+ **Constant** (primitive type && project/file/class-scoped) ```SNAKE_CASE | All caps```: *BTN_SELECTOR*
+ **Constant** (reference type || function-scoped) ```camelCase```

### 2 - Type & Function
+ **Function** ```camelCase```: *disableBtn()*
+ **Function** (async) ```camelCase | Async suffix``` *fetchUsersAsync()*
+ **Function** (in C#|Unity; C++|Unreal Engine) ```PascalCase```: *DisableBtn()*
+ **Class/struct/record** ```PascalCase```: *CoolBtn*
+ **Interface** ```PascalCase | I prefix```: *IClickable*
+ **Enum** ```PascalCase | Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ **Event** (of current class) ```camelCase | on+{ordinal}+{action}```: *onClick()*, *on1stClick()*
+ **Event** (of other object) ```camelCase | on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
+ **CSS class** ```BEM```: *hero__btn--round* ([reference](https://sparkbox.com/foundry/bem_by_example))

### 3 - Git
+ **Repo name** ```kebab-case | All lower``` (avoid lowerscore _ which seems bad for URL)  
#### Commit message
+ **Initial commit** first commit of the project involving common/familiar setup.
+ **[Exp]** experimenting, trying out a feature. This code can be used for reference later and removed when getting familiar (marked with // REMOVE).
+ **[Refactor]** refactoring code, removing unnecesary code/comments, reorganinzing code/files, etc.
+ **[Fix]**
+ **[Test]**
+ **[Doc]**

<a name="commenting"></a>  
# III - Commenting
[⬆ To the top](#0)
### 1 - Document
+ **Variable**: same line
```
public string cookie; // this meta tag has been deprecated in M63
```
+ **Output**

Result of single statement: same line
```
console.log('foobar') // expected output: foobar
```
Result of block of statements: below
```
const a = 'foo'
const b = 'bar'
console.log(a + b)
// expected output: foobar
```
+ **Function/block**: above 
```
// this does...
function fooBar(){}
```
+ **Ordered procedure**: above each line w/ cardinal numbers	
```
// 1. Create an interface representing a document in MongoDB
inteface User { name: string...
// 2. Create a Schema corresponding to the document interface
const schema = new Schema<User>({...
// 3...
```
+ **Mixed procedure**: above the procedure + mark according line w/ cardinal numbers	

```
/**
 * Main content containers
 * 1. Make the container full-width with a maximum width
 * 2. Center it in the viewport
 * 3. Leave some space on the edges, especially valuable on small screens
 */
.container {
  max-width: $max-width; /* 1 */
  margin-left: auto; /* 2 */
  margin-right: auto; /* 2 */
  padding-left: 20px; /* 3 */
  padding-right: 20px; /* 3 */
  width: 100%; /* 1 */
}
```
  
### 2 - Task
+ **TODO** general tasks
+ **FIX**
+ **REMOVE** the code is used for reference later and removed when becoming unneccesary.
+ **ADHOC** temporary code needed to be replaced by more elegant solutions.
+ **UTIL** utility/helper method should be moved into a dedicated file.
+ **REFACTOR** - **DRY** - **PARAMETERIZE**
+ **SPECIFIC** the code inside a general framework/library to solve problems for only a specific project, should be moved into that very project
  
### 3 - Section
> Use **upper case** to search by matched case in files (esp. CSS files) containing many categorizes, components, etc. 
+ **Categorize** containing multiple components
```
/*-------------------------
      BASIC COMPONENTS
-------------------------*/
```
```
///////////////////////////
//    BASIC COMPONENTS
```
+ **Component**
```
/* BUTTON */
```

<a name="architecture"></a>  
# IV - Architecture
[⬆ To the top](#0)
> Standard approaches to structure & organize code files
+ **SASS** ```7-1 pattern``` ([reference](https://www.learnhowtoprogram.com/user-interfaces/building-layouts-preprocessors/7-1-sass-architecture))
+ **TS & NodeJS** ([reference](https://github.com/microsoft/TypeScript-Node-Starter))


<a name="refactoring"></a>  
# V - Refactoring
[⬆ To the top](#0)
> Alternative ways of writing code to help improving **code readability, clarity, brevity & performance**  

**[Refactoring in C#](CS.md#preferences)**  
**[Refactoring in C++](CPP.md#preferences)**  
**[Refactoring in C++ | Unreal Engine](CPP_UE.md#preferences)**  
**[Refactoring in Dart](DART.md#preferences)**  
**[Refactoring in Python](PYTHON.md#preferences)**  
**[Refactoring in TypeScript & JavaScript](TS_JS.md#preferences)**  

### Declaration, Initialization & Assignment
+ ~~Type annotation (explicit type)~~ => **type inference** (implicit type) for initializer expression and local variable [C++11 (auto), C# (var), TS (none), Dart (var)]
> Pros: shorthand especially for long type init, focus more attention on local variable name and value
```
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();
// preference
var instance = new AReallyReallyLooooongClass();

List<User> users = {User1, User2...};
foreach(User user in users)
// preference
foreach(var user in users)
```

+ Assign w/ nullable variable using **nullish coalescing operator (??)** *[C#, PHP, ES11]*
```
result = (a !== null && a !== undefined) ? a : b;
//shorthand
result = a ?? b
```
+ Assign w/ nullable variable using **short circuit evaluation** *[most languages]*
```
result = (a !== null && a !== undefined) ? a : b;
//shorthand
result = a || b
```
+ Assign default value for nullable variable using **logical nullish assigment operator (??=)** *[TS/JS, C#8]*
```
a ?? (a = b)
//shorthand
a ??= b
```
+ **Multiple variable declaration** _[ES, C#, Java]_
```
let a;
let b;
let c = 3;
//shorthand
let a, b, c = 3;
```
+ Assign multiple variables using **object destructuring/tuple** _[ES, C#]_
```
let a = 1;
let b = 2;
let c = 3;
//shorthand
[a, b, c] = [1, 2, 3]
```

+ Swap two variables using **XOR**
> Pros: avoid using third temporary variable
```
temp = a;
a = b;
b = temp;

// shorthand
a ^= b ^= a ^= b;
```
  
### Control Flow
+ **Guard clause/assert/precondition**: return early in special case; multiple return
> Pros: avoid nested statements, improve readability
```
function getInsuranceDeductible(insurance) {
  if (insurance.covered) {
    if (insurance.majorRepair) {
      return 500
    } else if (insurance.mediumRepair) {
      return 300
    } else {
      return 100
    }
  } else {
    return 0
  }
}

//preference (use daisy chaining ternary operator to shorten furthermore)
function getInsuranceDeductible(insurance) {
  if (!insurance.covered) return 0
  if (insurance.majorRepair) return 500
  if (insurance.mediumRepair) return 300

  return 100
}
```
+ **Ternary operator (? :)** *[most languages]*  

To assign value:
```
if (a > b) {
    result = x;
}
else {
    result = y;
}
//shorthand
result = a > b ? x : y;
```

To return:
```
if (a > b) {
    return x;
}
else {
    return y;
}
//shorthand
return a > b ? x : y;
```
Daisy chaining:
```
function getInsuranceDeductible(insurance) {
  if (!insurance.covered) return 0
  if (insurance.majorRepair) return 500
  if (insurance.mediumRepair) return 300

  return 100
}

//shorthand
function getInsuranceDeductible(insurance) {
  return insurance.covered ? 0
         : insurance.majorRepair ? 500
         : insurance.mediumRepair ? 300 
         : 100
}
```

+ Conditional w/ **truthy/falsy values** *[TS/JS, Groovy, Perl, PHP, Python, Ruby]*
```
if(typeof a !== "undefined" && typeof b !== "null" && typeof c !== "NaN" && d !== "" && array.length !== 0)
// shorthand
if(a && b && c && d && array.length)
```
+ Conditional w/ **short circuit evaluation** *[most languages]*
```
if(isHungry) {
  code()
}
// shorthand
isHungry && code()
```



### Expressions
+ ~~Equality operator (==)~~ => **Strict equality operator** (===) *[TS]*
+ **Spaceship/three-way comparison operator (<=>)** *[C++, Groovy, Kotlin, Perl, PHP, Ruby]*
```
$users = ['branko', 'ivana', 'luka', 'ivano'];

usort($users, function ($a, $b) {
  return ($a < $b) ? -1 : (($a > $b) ? 1 : 0);
});

//shorthand
usort($users, function ($a, $b) {
  return $a <=> $b;
});
```


  
### Type
+ **Constructor shorthand/property promotion** *[TS, PHP8]*
```
class User {
  private name: string;
  private age: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

//shorthand
class User {
  constructor(
    private name: string,
    private age: number
  ) {}
}
```



### Function
+ **Lambda expression/Arrow function (=>)** [Java8, JS/TS (fat arrow), Dart, C# (expression-bodied members)]

To declare single statement functions
> Pros: bind _this_ to the invoker
```
function getSum(a: number, b: number) {
  return a + b
}
// shorthand
const getSum = (a: number, b: number) => (a + b)
```

To pass a function as an argument (**anonymous function**)
> Pros: no need to declare a separate function -> reduce coding overheating


+ **Named parameters** *[PHP, Kotlin, C#]*
> Reason: for clarity, can change order of params
```
public void doSomething(string foo, int bar) {...}

doSomething("someString", 1);
//preference
doSomething(foo: "someString", bar: 1);
```
+ ~~Overloading functions~~ that differ only in trailing parameters => **optional parameters**
```
interface Example {
  diff(one: string): number;
  diff(one: string, two: string): number;
  diff(one: string, two: string, three: boolean): number;
}

//shorthand
interface Example {
  diff(one: string, two?: string, three?: boolean): number;
}
```

+ ~~Promise/callback chaining~~ => **async-await** *[ES6, C#, Dart]*


### String
+ ~~String~~ => **StringBuffer** for string appending *[Java, C#]*
+ ~~String concatenation operator (+)~~ => **String interpolation/template literals** *[ES, C#, Kotlin, PHP]*
```
console.log("Sum of " + a + " and " + b + " is " + (a + b))
// preference
console.log(`Sum of ${a} and ${b} is ${a + b}`)
```

