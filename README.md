# Table of Contents
1. [Naming](#1)
2. [Commenting](#2)
3. [Preference](#3)
4. [Shorthand](#4)
5. [Git](#5)

<a name="1"></a>  
# I - Naming

### 1.1 - General
+ **Constant** (primitive type && project/file/class-scoped) ```SNAKE_CASE | All caps```: *BTN_SELECTOR*
+ **Function/variable/constant** (reference type || function-scoped) ```camelCase```: *disableBtn()*
+ **Class/struct/record** ```PascalCase```: *CoolBtn*
+ **Interface** ```PascalCase | I prefix```: *IClickable*
+ **Enum** ```PascalCase | Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ **Event** ```camelCase | on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
+ **CSS class** ```BEM```: *hero__btn--round* ([reference](https://sparkbox.com/foundry/bem_by_example))
  
### 1.2 - Variable
+ **Element/HTMLElement** ```e prefix```: *eBtn*
+ **NodeListOf\<Element>** ```es prefix```: *esBtn* (questionable?)
+ **JQuery\<HTMLElement>** ```$ prefix```: *$btn* (questionable?)
+ **Boolean** ```{tobe}+{noun}+{adj/verb-ed}```: *wasBtnClicked*, *areBtnsGreen*
+ **Private class member** ```_ prefix```: *_id* (questionable?)
  
### 1.3 - Abbreviation
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

<a name="2"></a>  
# II - Commenting
  
### 2.1 - Document
+ **Function/block/statement**: on the above line
```
// this does...
function fooBar(){}
```
+ **Variable**: on the same line
```
public string cookie; // this meta tag has been deprecated in M63
```
+ **Output**: on the below line
```
console.log('foo bar');
// expected output: foo bar
```
+ **Procedure**: on the above lines with 1, 2, 3...
```
// 1. Create an interface representing a document in MongoDB
inteface User { name: string...
// 2. Create a Schema corresponding to the document interface
const schema = new Schema<User>({...
...
```
  
### 2.2 - Task
+ **TODO** general tasks
+ **FIX**
+ **REMOVE** the code is used for reference later and removed when becoming unneccesary.
+ **ADHOC** temporary code needed to be replaced by more elegant solutions.
+ **UTIL** utility/helper method should be moved into a dedicated file.
+ **REFACTOR** - **DRY** - **PARAMETERIZE**
+ **SPECIFIC** the code inside a general framework/library to solve problems for only a specific project, should be moved into that very project
  
### 2.3 - Section
> Use **upper case** to search by matched case in files containing many categorizes, components, etc. (esp CSS file)
+ **Categorize** containing multiple components
```
/*-------------------------
      BASIC COMPONENTS
-------------------------*/
```
+ **Component**
```
/* BUTTON */
```

<a name="3"></a>  
# III - Preference
> Alternative ways of doing stuffs but help improving **code readability & clarity**
+ ~~Enum~~ => **Union types** ([reference](https://fettblog.eu/tidy-typescript-avoid-enums/?fbclid=IwAR18SiWtUFai4gEY4B6rm2nSGYfR54Yw3bitrkl4Ph9z72qwM_8kbOUYhX8)) *[TS]*
+ ~~Equality operator (==)~~ => **Strict equality operator** (===) *[TS]*
+ ~~Promise/callback chaining~~ => **async-await** *[ES6]*
+ ~~try-finally~~ => **using** *[C#]*
+ **Object initializer/builder** [C#]*
+ **Object destructuring** *[TS/JS]*
+ **Named arguments** *[PHP, Kotlin]*
+ **Guard clause/assert/precondition**
+ ~~String~~ => **StringBuffer** for string appending *[Java, C#]*
+ ~~String concatenation operator (+)~~ => **String interpolation/template** *[TS/JS, Kotlin, PHP]*
```
console.log("Sum of " + a + " and " + b + " is " + (a + b))
// preference
console.log(`Sum of ${a} and ${b} is ${a + b}`)
```

<a name="4"></a>  
# IV - Shorthand
> Recommend to utilize following features if available in the using language for **code brevity**
+ **Ternary operator (? :)** *[most languages]*
```
if (a > b) {
    result = x;
}
else {
    result = y;
}
// shorthand
result = a > b ? x : y;
```
+ **Nullish coalescing operator (??)** *[C#, PHP, ES11]*
```
result = (a !== null && a !== undefined) ? a : b;
// shorthand
result = a ?? b
```
+ **Logical nullish assigment operator (??=)** *[TS/JS]*
```
a ?? (a = b)
// shorthand
a ??= b
```
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
// shorthand
class User {
  constructor(
    private name: string,
    private age: number
  ) {}
}
```
+ **Object property value shorthand** *[ES6]*
```
let cat = 'Miaow';
let dog = 'Woof';
let bird = 'Peet peet';

var myPets = {
  cat: cat,
  dog: dog,
  bird: bird
}
//shorthand
let myPets = {
  cat,
  dog,
  bird
}
```
+ **Spaceship/three-way comparison operator (<=>)** *[C++, Groovy, Kotlin, Perl, PHP, Ruby]*
```
$users = ['branko', 'ivana', 'luka', 'ivano'];

usort($users, function ($a, $b) {
  return ($a < $b) ? -1 : (($a > $b) ? 1 : 0);
});
// shorthand
usort($users, function ($a, $b) {
  return $a <=> $b;
});
```
+ **Lambda expression/Arrow function (=>)** *[Java8, ES6, Dart]*
```
function getSum(a: number, b: number) {
  return a + b
}
// shorthand
const getSum = (a: number, b: number) => (a + b)
```
+ If conditional w/ **truthy/falsy values** *[TS/JS, Groovy, Perl, PHP, Python, Ruby]*
```
if(typeof a !== "undefined" && typeof b !== "null" && typeof c !== "NaN" && d !== "" && array.length !== 0)
// shorthand
if(a && b && c && d && array.length)
```
+ **Implicit typing (var)**: for long named type *[C#]*
```
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();
// shorthand
var instance = new AReallyReallyLooooongClass();
```
+ Concise **new** *[C#9]* 
```
ExampleClass instance = new ExampleClass();
// shorthand
ExampleClass instance = new();
```

<a name="5"></a>  
# V - Git
+ **Repo name** ```kebab-case | All lower``` (avoid lowerscore _ which seem bad for URL)
  
### Commit message
+ **Initial commit** first commit of the project involving common/familiar setup.
+ **[Exp]** experimenting, trying out a feature. This code can be used for reference later and removed when getting familiar (marked with // REMOVE).
+ **[Refactor]** refactoring code, removing unnecesary code/comments, reorganinzing code/files, etc.
+ **[Fix]**
+ **[Test]**
+ **[Doc]**
