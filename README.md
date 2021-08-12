# Naming
+ Constant: BUTTON_SELECTOR
+ Interface: IClickable
+ Enum: ButtonState {Clicked, Forcus, Hover, Active}
### Variable
+ Element/HTMLElement: eButton
+ NodeListOf\<Element>: esButton
+ JQuery\<HTMLElement>: $button (questionable?)
+ boolean: ```{tobe}+{noun}+{adj/verb-ed}``` wasButtonClicked, areButtonsGreen
### Abbreviation
+ Background: bg
### Event
+ ```on+{noun}+{action}```: onBgChange
+ Trigger at 1st/2nd... time: onBgFirstChange

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
+ // REFACTOR
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
