# 1. Naming
+ **Constant** (primitive type && project/file/class-scoped) ```SNAKE_CASE | All caps```: *BTN_SELECTOR*
+ **Function/variable/constant** (reference type || function-scoped) ```camelCase```: *disableBtn()*
+ **Class/struct/record** ```PascalCase```: *CoolBtn*
+ **Interface** ```PascalCase | I prefix```: *IClickable*
+ **Enum** ```PascalCase | Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ **Event** ```camelCase | on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
  
### Variable
+ **Element/HTMLElement** ```e prefix```: *eBtn*
+ **NodeListOf\<Element>** ```es prefix```: *esBtn* (questionable?)
+ **JQuery\<HTMLElement>** ```$ prefix```: *$btn* (questionable?)
+ **Boolean** ```{tobe}+{noun}+{adj/verb-ed}```: *wasBtnClicked*, *areBtnsGreen*
+ **Private class member** ```_ prefix```: *_id* (questionable?)
  
<details>
      <summary><b>Abbreviation</b></summary>
<br>
      
* **addr** address
* **app** application
* **bg** background
* **btn** button
* **char** character
* **col** column
* **coord** coordinate
* **db** database
* **dest** destination
* **dir** directory
* **len** length
* **msg** message
* **num** number
* **obj** object
* **pwd** password
* **param** parameter
* **pic** picture
* **pos** position
* **str** string
* **src** source
* **val** value
* **var** variable
      
</details>


# 2. Commenting
  
### Document
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
  
### Task
+ **TODO** general tasks
+ **FIX**
+ **REMOVE** the code is used for reference later and removed when becoming unneccesary.
+ **ADHOC** temporary code needed to be replaced by more elegant solutions.
+ **UTIL** utility/helper method should be moved into a dedicated file.
+ **REFACTOR** - **DRY** - **PARAMETERIZE**
+ **SPECIFIC** the code inside a general framework/library to solve problems for only a specific project, should be moved into that very project
  
### Section
> Use upper case to search by matched case in files containing many categorizes, components, etc.
+ **Categorize**
```
/*-------------------------
      BASIC COMPONENTS
-------------------------*/
```
+ **Component**
```
/* BUTTON */
```

# 3. Preference
> Alternative ways of doing stuffs but help improving **code readability & clarity**
+ ~~Enum~~ => **Union types** ([reference](https://fettblog.eu/tidy-typescript-avoid-enums/?fbclid=IwAR18SiWtUFai4gEY4B6rm2nSGYfR54Yw3bitrkl4Ph9z72qwM_8kbOUYhX8)) *[TS]*
+ ~~Equality operator (==)~~ => **Strict equality operator** (===) *[TS]*
+ ~~Promise/callback chaining~~ => **async-await** *[TS/JS]*
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

# 4. Shorthand
> Recommend to utilize following features if available in the using language for **code brevity**
+ **Ternary operator** *[most languages]*
+ **Nullish coalescing operator** *[C#, PHP, TS]*
+ **Logical nullish assigment** *[TS]*
+ **Constructor shorthand/property promotion** *[TS, PHP]*
+ **Object property shorthand** *[TS/JS]*
+ If conditional w/ **truthy/falsy values** *[TS/JS, Groovy, Perl, PHP, Python, Ruby]*
```
if(typeof a !== "undefined" && typeof b !== "null" && typeof c !== "NaN" && d !== "" && array.length !== 0)
// shorthand
if(a && b && c && d && array.length)
```
+ Implicit typing - **var**: for long named type *[C#]*
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

# 5. Git
+ **Repo name** ```kebab-case | All lower``` (avoid lowerscore _ which seem bad for URL)
  
### Commit message
+ **Initial commit** first commit of the project involving common/familiar setup.
+ **[Exp]** experimenting, trying out a feature. This code can be used for reference later and removed when getting familiar (marked with // REMOVE).
+ **[Refactor]** refactoring code, removing unnecesary code/comments, reorganinzing code/files, etc.
+ **[Fix]**
+ **[Test]**
+ **[Doc]**
