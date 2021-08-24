# C#

## Preferences
+ Check for nullity using **is** & **is not** _[C#9]_
```
if (a == null && b != null)
// preference
if (a is null && b is not null)
```
