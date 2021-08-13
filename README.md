# Naming
+ Constant (project/file/class-scoped) ```SNAKE_CASE | All caps```: *BTN_SELECTOR*
+ Function/variable/constant (function-scoped) ```camelCase```: *disableBtn()*
+ Class ```PascalCase```: *CoolBtn*
+ Interface ```PascalCase | I_```: *IClickable*
+ Enum ```PascalCase | Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ Event ```camelCase | on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
### Variable
+ Element/HTMLElement ```e_```: *eBtn*
+ NodeListOf\<Element> ```es_```: *esBtn* (questionable?)
+ JQuery\<HTMLElement> ```$_```: *$btn* (questionable?)
+ Boolean ```{tobe}+{noun}+{adj/verb-ed}```: *wasBtnClicked*, *areBtnsGreen*
+ Private class member ```_```: *_id* (questionable?)

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
* **param** parameter
* **pic** picture
* **pos** position
* **str** string
* **src** source
* **val** value
* **var** variable
      
</details>


# Commenting
### Document
+ Function/block/statement: on the above line
```
// this does...
function fooBar(){}
```
+ Variable: on the same line
```
public string cookie; // this meta tag has been deprecated in M63
```
+ Output: on the below line
```
console.log('foo bar');
// expected output: foo bar
```
+ Procedure: on the above lines with 1, 2, 3...
```
// 1. Create an interface representing a document in MongoDB
inteface User { name: string...
// 2. Create a Schema corresponding to the document interface
const schema = new Schema<User>({...
...
```
### Task
+ // TODO: general tasks
+ // FIX
+ // REMOVE: the code is used for reference later and removed when becoming unneccesary.
+ // ADHOC: temporary code needed to be replaced by more elegant solutions.
+ // UTIL: utility/helper method should be moved into a dedicated file.
+ // REFACTOR - // DRY - // PARAMETERIZE
+ // SPECIFIC: the code inside a general framework/library to solve problems for only a specific project, should be moved into that very project
### Section
> Use upper case to search by matched case in files containing many categorizes, components, etc.
+ Categorize:
```
/*-------------------------
      BASIC COMPONENTS
-------------------------*/
```
+ Component:
```
/* BUTTON */
```

# Git
+ Repo name ```kebab-case | All lower``` (avoid lowerscore _ which seem bad for URL)
### Commit message
+ **Initial commit** first commit of the project involving common/familiar setup.
+ **[Exp]** experimenting, trying out a feature. This code can be used for reference later and removed when getting familiar (marked with // REMOVE).
+ **[Refactor]** refactoring code, removing unnecesary code/comments, reorganinzing code/files, etc.
+ **[Fix]**
+ **[Test]**
+ **[Doc]**
