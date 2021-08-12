# Naming
+ Constant ```SNAKE_CASE```: *BTN_SELECTOR*
+ Function/variable ```camelCase```: *disableBtn()*
+ Class ```PascalCase```: *CoolBtn*
+ Interface ```I_```: *IClickable*
+ Enum ```PascalCase-Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ Event ```on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
### Variable
+ Element/HTMLElement ```e_```: *eBtn*
+ NodeListOf\<Element> ```es_```: *esBtn* (questionable?)
+ JQuery\<HTMLElement> ```$_```: *$btn* (questionable?)
+ boolean: ```{tobe}+{noun}+{adj/verb-ed}``` *wasBtnClicked*, *areBtnsGreen*

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
### Task
+ // TODO: general tasks
+ // REFACTOR - // DRY - // PARAMETERIZE
+ // UTIL: helper method to move into a dedicated file
+ // FIX
+ // REMOVE 
+ Project-specific
### Section
> Use upper case to search by matched case in files containing many categorizes, components...
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
