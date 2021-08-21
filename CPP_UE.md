# C++ In Unreal Engine

## Preference
+ Concatenate string w/ **format specifier**
```
FString name = "John";
int32 age = 18;
FString::Printf(TEXT("%s is %i years old."), *name, age); //output: Jorn is 18 years old
```
