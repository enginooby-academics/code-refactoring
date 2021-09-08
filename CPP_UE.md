# C++ In Unreal Engine

## String
+ Concatenate string w/ **format specifier**
```cpp
FString name = "John";
int32 age = 18;
FString::Printf(TEXT("%s is %i years old."), *name, age); //output: Jorn is 18 years old
```
