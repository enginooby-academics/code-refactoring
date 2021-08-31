# C#

## Preferences
+ Check for nullity using **pattern matching (is, is not)**_[C#7]_
```
if (a == null && b != null)
// preference
if (a is null && b is not null)
```
+ ~~Class/Struct~~ => **Record**: for immutable data models _[C#9]_ ([reference](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#record-types))
+ ~~set accessor~~ => **init accesor**: for immutable properties in class/struct/record _[C#9]_ ([reference](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#init-only-setters))
```
class User {
    public string Name {get; set};
    public int Age {get; init};
}

User user = new() {Name = "John", age = 18};
user.Name = "John Ritter"; // no error
user.Age = 20; // error! CS8852.
```
+ Prefer **object initializer syntax** than overloading constructors or invoking multiples setters ([reference](https://stackoverflow.com/a/740682))
+ **Digit separators**: for long numbers _[C#7]_
```
public const long BillionsAndBillions = 100000000000;
// preference
public const long BillionsAndBillions = 100_000_000_000;
```
+ Use **readonly** for members which don't modify state, e.g. ```ToString()``` _[C#8]_ ([reference](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-8#readonly-members))  
> Reason: this feature specifies the design intent so the compiler can enforce it, and make optimizations based on that intent.
+ Use **partial class** to split the implementation of different interfaces
```
partial class MyClass
{
    // main implementation of MyClass
}


partial class MyClass : IF1
{
    // implementation of IF1
}

partial class MyClass : IF2
{
    // implementation of IF2
}
```
+ ~~Region directive (#region)~~
> Reason: Regions are considered anti-patterns. They require more work which doesn’t increase the quality or readability of the code, reduce the number of bugs, and makes the code more complicated to refactor.
+ Create **extension methods** for commonly used operations on value types or existing classes  
> Reason: reduce one parameter in utility method for value types, add new functions for a class without modifying/inheriting it
```
namespace ExtensionMethods;

public static class IntUtils
{
    public static bool IsGreaterThan(this int i, int value) => i > value;
    public static bool IsPrime...
}

public static class StringUtils
{
    public static int GetWordCount(this string word) => str.Split(new char[] { ' ', '.', '?' }, StringSplitOptions.RemoveEmptyEntries).Length;
}
```
Usage:  
```
using ExtensionMethods;

int i = 5;
if(i.IsGreaterThan(3)) System.Console.WriteLine($"{i} is greater than 3"); // output: 5 is greater than 3

string name = "Foo Bar";
System.Console.WriteLine(name.GetWordCount()); // output: 2
```
+ ~~POCO class~~ => **tuple**: for returning multiple values from private and internal utility methods _[C#7]_
+ ~~Base type casting~~ => **System.Convert** 
> Reason: Convert class enables to convert between non-compatible types
```
string variable = "5.00"; 

double varDouble = (double)variable; // error: InvalidCastException
double varDouble = System.Convert.ToDouble(variable); // no error
```
+ ~~Objest casting~~ => **as**
> Reason: if non-comatible types, casting throws InvalidCastException while as return null  
> Con: potential to get NullReferenceException later
```
User instance = (User) mobileUser;
//preference
User instance = mobileUser as User;
```
~~System.Collections.ArrayList~~ => **generic collection** (System.Collections.Generic.List<T>)
> Reason: avoid boxing/unboxing => reduce workload of Garbabe Collection => increase performance
+ Use **nameof()** to address class/function/param name in string
> Reason: when changing name, the corresspond values in string will update as well
```
public void PrintUserName(User currentUser)
{
    //The refactoring tool might miss the textual reference to current user below if we're renaming it
    currentUser is null && _logger.Error("Argument currentUser is not provided");
    
    //preference
    currentUser is null && _logger.Error($"Argument {nameof(currentUser)} is not provided");
}    
```
+ Use **Equals() & OrdinalIgnoreCase** to compare strings regardless of case
> Pro: removes the additional string allocation overhead
```
str1.ToUpper() == str2.ToUpper()
//preference
str1.Equals(str2, StringComparison.OrdinalIgnoreCase)
```
    
    
    
    
## Shorthands
+ **Switch expressions** _[C#8]_
```
enum BankStatus {Open, Closed, VIPOnly};

static bool CheckIfCanWalkIntoBankSwitch(BankStatus bankStatus, bool isVip)
{
    bool result = false;

    switch(bankStatus)
    {
        case BankStatus.Open : 
            result = true;
            break;
        case BankStatus.Closed : 
            result = false;
            break;       
        case BankStatus.VIPCustomersOnly : 
            result = isVip;
            break;
        default:
            throw new ArgumentException(message: "invalid enum value"),
    }

    return result;
}

// shorthand (w/ arrow function)
static bool CheckIfCanWalkIntoBank(BankStatus bankStatus, bool isVip) => bankStatus switch
{
    BankBranchStatus.Open => true, 
    BankBranchStatus.Closed => false, 
    BankBranchStatus.VIPCustomersOnly => isVip,
    _ => throw new ArgumentException(message: "invalid enum value")
};
```
+ **Implicit typing (var)**: for long named type
```
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();
// shorthand
var instance = new AReallyReallyLooooongClass();
```
+ Declare nullable type w/ **T?**
```
Nullable<int> num = null;
// shorthand
int? num = null;
```
+ **Concise new (new())** *[C#9]* 
```
ExampleClass instance = new ExampleClass();
// shorthand
ExampleClass instance = new();
```
+ **Automatic properties**
```
class User {
    //longhand
    private string _name;
    public string Name {
        get {return _name}
        set (_name = value}
    }
    
    //shorthand
    public string Name {get; set}
}
```
+ **Top-level statement**: compact Main method _[C#9]_ ([reference](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#top-level-statements))
```
using System;
namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
// shorthand
using System;
Console.WriteLine("Hello World!");
```
+ **File-scoped namespace declaration** _[C#10]_
```
namespace ApplicationA {
    class User {
        ...
    }
}
// shorthand
namespace ApplicationA;
class User {
    ...
}
```
+ **Namespace alias qualifier (::)**
```
namespace ApplicationA;
class User {}
```
```
namespace ApplicationB;
class User {}
```
Main 
```
using A = ApplicationA;
using B = ApplicationB;

A::User = new();
B::User = new();
```
+ **Aliased generics (using)**
```
Dictionary<string, Dictionary<string, List<string>>> User1 = new();
Dictionary<string, Dictionary<string, List<string>>> User2 = new();

//shorthand
using ASimpleName = Dictionary<string, Dictionary<string, List<string>>>;
ASimpleName User1 = new();
ASimpleName User2 = new();
```
+ Use **from end operator (^)** & **range operator (..)** for sequence/collection _[C#8])_ ([reference](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/ranges-indexes#language-support-for-indices-and-ranges))
```
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0

// access element
Console.WriteLine($"The last word is {words[words.Length - 1]}");
Console.WriteLine($"The second last word is {words[words.Length - 2]}");
// shorthand
Console.WriteLine($"The last word is {words[^1]}");
Console.WriteLine($"The second last word is {words[^2]}");

// extract elements
string[] quickBrownFox = new string[] {words[1], words[2], words[3]};
// shorthand
string[] quickBrownFox = words[1..4];
// other examples
string[] allWords = words[..];
string[] lazyDog = words[^2..^0];
string[] theLazyDog = words[6..];
```
+ Initialize collections using **collection initializer syntax**
```
List<string> users = new();  
users.Add("User 1");  
users.Add("User 2");

// shorthand
List<string> users = new() {"User 1", "User 2");
```
+ Use **tuple** in class constructor _[C#7]_
```
class User {
    public string Name {get; set};
    public int Age {get; set};
    
    // longhand
    public User(string name, int age){
        _name = name;
        _age = age;
    }
    
    // shorthand
    public User(string name, int age) => (_name, _age) = (name, age);
}
```
+ ~~Escaped characters~~ => **verbatim string (@)**
```
string myFileName = "C:\\myfolder\\myfile.txt";
//shorthand
string myFileName = @"C:\myfolder\myfile.txt";
   
```
+ **String methods**
```
// Indicates whether the specified string is null or an Empty string.
string.IsNullOrEmpty(string value);

// Indicates whether a specified string is null, empty, or consists only of white-space characters.
string.IsNullOrWhiteSpace(string value);
```
