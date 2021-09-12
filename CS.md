# C#
<a name="0"></a>  
### Table of Contents
+ [Declaration, Initialization & Assignment](#init)  
+ [Control Flow](#_control-flow)
+ [Expressions](#_expressions)
+ [Function](#_function)
+ [OOP](#_oop)
+ [String](#_string)
+ [Numeric](#_numeric)
+ [Collection](#_collection)
+ [Others](#_others)

<a name="init"></a>      
### Declaration, Initialization & Assignment
[⬆ To the top](#0)
+ **Implicit typing ```var```**: for long named type
```csharp
// 👎 longhand
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();

// 👍 shorthand
var instance = new AReallyReallyLooooongClass();
```

+ Declare nullable type w/ **```T?```**
```csharp
// 👎 longhand
Nullable<int> num = null;

// 👍 shorthand
int? num = null;
```

+ Init object using **target-typed new expressions ```new()```** [[C#9](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-9.0/target-typed-new)] 
```csharp
// 👎 longhand
ExampleClass instance = new ExampleClass();

// 👍 shorthand
ExampleClass instance = new();
```

+ Prefer **object initializer syntax** than overloading constructors or invoking multiples setters [[Reference](https://stackoverflow.com/a/740682)]
```csharp
// 👎 non-compliant
User user1 = new();
user1.Name = "User 1";
user1.Age = 18;

// 👍 preference
User user1 = new {Name: "User 1"; Age: 18};
```

+ Copy then modify record instance using **with expression** [[C#9](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/with-expression)]
```csharp
// 👉 given
User user1 = new {Name: "User 1"; Age: 18};

// 👎 longhand
User user2 = user1;
user2.Name = "User 2";

// 👍 shorthand
User user2 = user1 with {Name = "User 2");
```

+ Init collection using **collection initializer syntax**
```csharp
// 👎 longhand
List<string> users = new();  
users.Add("User 1");  
users.Add("User 2");

// 👍 shorthand
List<string> users = new {"User 1", "User 2");
```



<a name="_control-flow"></a>      
### Control Flow
[⬆ To the top](#0)
+ **Switch expressions** [[C#8](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-8#switch-expressions)]
```csharp
// 👎 longhand
switch (DateTime.Now.DayOfWeek)
{
    case DayOfWeek.Monday:
        return "Not Weekend";
    case DayOfWeek.Tuesday:
        return "Not Weekend";
    case DayOfWeek.Wednesday:
        return "Not Weekend";
    case DayOfWeek.Thursday:
        return "Not Weekend";
    case DayOfWeek.Friday:
        return "Not Weekend";
    case DayOfWeek.Saturday:
        return "Weekend";
    case DayOfWeek.Sunday:
        return "Weekend";
    default:
        throw new ArgumentOutOfRangeException();
}

// 👍 shorthand
DateTime.Now.DayOfWeek switch
{
    DayOfWeek.Monday => "Not Weekend",
    DayOfWeek.Tuesday => "Not Weekend",
    DayOfWeek.Wednesday => "Not Weekend",
    DayOfWeek.Thursday => "Not Weekend",
    DayOfWeek.Friday => "Not Weekend",
    DayOfWeek.Saturday => "Weekend",
    DayOfWeek.Sunday  => "Weekend",
    _ => throw new ArgumentOutOfRangeException()
}

// 👍👍 shorthand with pattern (not)
DateTime.Now.DayOfWeek switch
{
    not (DayOfWeek.Saturday or DayOfWeek.Sunday) => "Not Weekend",
    DayOfWeek.Saturday or DayOfWeek.Sunday => "Weekend",
    _ => throw new ArgumentOutOfRangeException()
}
```



<a name="_expressions"></a>      
### Expressions
[⬆ To the top](#0)
> Used with control flow (if expression, switch case expression), = expression, return expression
+ ~~==, !=, &&, ||~~ => **pattern matching ```is``` & pattern combinators ```not, and, or```** [[C#7](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-7#pattern-matching)]

Check type:
```csharp
if (a is int)
```

Check null:
```csharp
// 👉 given
User? user = null;

// 👎 non-compliant
if(!user.HasValue)
if(user == null)

// 👍 preference
if(user is null)
```

+ Check equality for nullable objects using **```Object.Equals()```**

```csharp
// 👎 longhand
if ((user1 == user2) || ((user1 != null and user2 != null) and user1.Equals(user2)))

// 👍 shorthand
if(Object.Equals(user1, user2))
```

+ Use **```Equals() & OrdinalIgnoreCase```** to compare strings regardless of case
> ✔️ Pros: removes the additional string allocation overhead
```csharp
// 👎 non-compliant
str1.ToUpper() == str2.ToUpper()

// 👍 preference
str1.Equals(str2, StringComparison.OrdinalIgnoreCase)
```



<a name="_oop"></a>      
###  OOP
[⬆ To the top](#0)
+ ~~Class/Struct~~ => **Record**: for DTO [[C#9](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#record-types)]
> ✔️ Pros: reference type, immutable by default

+ **Automatic properties**
```csharp
class User {
    // 👎 longhand
    private string _name;
    public string Name {
        get {return _name}
        set (_name = value}
    }
    
    // 👍 shorthand
    public string Name {get; set}
}
```

+ ~~set accessor~~ => **init accesor**: for immutable properties in class/struct/record [[C#9](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#init-only-setters)]
```csharp
class User {
    public string Name {get; set};
    public int Age {get; init};
}

User user = new {Name = "John", age = 18};
user.Name = "John Ritter"; // no error
user.Age = 20; // error! CS8852.
```

+ Use **```readonly```** for members which don't modify state, e.g. ```ToString()``` [[C#8](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-8#readonly-members)]
> ✔️ Pros: specifies the design intent so the compiler can enforce it, and make optimizations based on that intent.

+ Use **partial class** to split the implementation of different interfaces
```csharp
// 📄 MyClass.cs
partial class MyClass{}

// 📄 MyClassIF1.cs
partial class MyClass : IF1 {}

// 📄 MyClassIF2.cs
partial class MyClass : IF2 {}
```

+ Use **tuple** in class constructor [C#7]
```csharp
class User {
    public string Name {get; set};
    public int Age {get; set};
    
    // 👎 longhand
    public User(string name, int age){
        _name = name;
        _age = age;
    }
    
    // 👍 shorthand
    public User(string name, int age) => (_name, _age) = (name, age);
}
```



<a name="_function"></a>      
### Function
[⬆ To the top](#0)
+ Create **extension methods** for commonly used operations on value types or existing classes  
> ✔️ Pros: reduce one parameter in utility method for value types, add new functions for a class without modifying/inheriting it
```csharp
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
```csharp
using ExtensionMethods;

int i = 5;
if(i.IsGreaterThan(3)) System.Console.WriteLine($"{i} is greater than 3"); // output: 5 is greater than 3

string name = "Foo Bar";
System.Console.WriteLine(name.GetWordCount()); // output: 2
```

+ **Implicit method group conversion** for callback function
```csharp
// 👉 given
List<string> users = new {"User 1", "User 2"};

// 👎 longhand
users.ForEach(user => Console.WriteLine(user));

// 👍 shorthand
users.ForEach(Console.WriteLine);
```

+ ~~POCO class~~ => **tuple**: for returning multiple values from private and internal utility methods [C#7]



<a name="_string"></a>      
### String
[⬆ To the top](#0)
+ Use **```nameof()```** to address class/function/param name in string
> ✔️ Pros: when changing name, the corresspond values in string will update as well
```csharp
public void PrintUserName(User currentUser)
{
    // 👎 the refactoring tool might miss the textual reference to current user below if we're renaming it
    currentUser is null && _logger.Error("Argument currentUser is not provided");
    
    // 👍 preference
    currentUser is null && _logger.Error($"Argument {nameof(currentUser)} is not provided");
}    
```

+ ~~""~~ => **```String.Empty```**

+ ~~Escape sequence~~ => **verbatim string ```@```**
```csharp
// 👎 non-compliant
string myFileName = "C:\\myfolder\\myfile.txt";

// 👍 preference
string myFileName = @"C:\myfolder\myfile.txt";
```

+ **String methods**
```csharp
// whether the specified string is null or an Empty string.
String.IsNullOrEmpty(string value);

// whether a specified string is null, empty, or consists only of white-space characters.
String.IsNullOrWhiteSpace(string value);
 
List<string> users = new {"User 1", "User 2"};
String.Join(",", users);
```



<a name="_numeric"></a>      
### Numeric
[⬆ To the top](#0)
+ **Digit separators**: for long numbers [C#7]
```csharp
// 👎 non-compliant
public const long BillionsAndBillions = 100000000000;

// 👍 preference
public const long BillionsAndBillions = 100_000_000_000;
```



<a name="_collection"></a>      
### Collection
[⬆ To the top](#0)  
+ ~~```System.Collections.ArrayList```~~ => **generic collection** ```System.Collections.Generic.List<T>```
> ✔️ Pros: avoid boxing/unboxing => reduce workload of Garbabe Collection => increase performance
    
+ ~~```Dictionary.ContainsKey()```~~ => **```Dictionary.TryGetValue()```**
> ✔️ Pro: thread-safety, more compact if check & get value
```csharp
// 👎 non-compliant
if(dictionary.ContainsKey(key)) 
{
    value = dictionary[key];
    ...
}
    
// 👍 preference
if(dictionary.TryGetValue(key, out value)) 
{ ... }
```    
    
+ Use **from end operator ```^```** w/ **range operator ```..```** for sequence/collection [[C#8](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/ranges-indexes#language-support-for-indices-and-ranges)]
```csharp
// 👉 given
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
```
    
To access collection element:
```csharp
// 👎 longhand
Console.WriteLine($"The last word is {words[words.Length - 1]}");
Console.WriteLine($"The second last word is {words[words.Length - 2]}");
    
// 👍 shorthand
Console.WriteLine($"The last word is {words[^1]}");
Console.WriteLine($"The second last word is {words[^2]}");
```
    
To extract elements:
```csharp
// 👎 longhand
string[] quickBrownFox = new string[] {words[1], words[2], words[3]};
    
// 👍 shorthand
string[] quickBrownFox = words[1..4];
    
// 👍 other examples
string[] allWords = words[..];
string[] lazyDog = words[^2..^0];
string[] theLazyDog = words[6..];
```
    
+ Make a collection of continuous integers using **```Enumerable.Range()```**
```csharp
// 👎 longhand
List<int> from2To8 = new {2, 3, 4, 5, 6, 7, 8};
    
// 👎 longhand
List<int> from2To8 = new();
for(int i = 2; i <= 8; i++) from2To8.Add(i);
                     
// 👍 shorthand
List<int> from2To8 = Enumerable.Range(2, 8).ToList();
```

+ Return empty collection using **```Enumerable.Empty<T>()```** or **```Array.Empty<T>()```**
> ✔️ Pros: reusable empty instance
```csharp
// 👎 non-compliant
return null; // 1: force to check null
return new List<User>(); // 2: increase the pressure on the Garbage Collector
    
// 👍 preference
return Enumerable.Empty<User>();
```
    

<a name="_others"></a>      
### Others
[⬆ To the top](#0)
+ **Top-level statement**: compact Main method [[C#9](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#top-level-statements)]
```csharp
// 👎 longhand
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
    
// 👍 shorthand
using System;
Console.WriteLine("Hello World!");
```
    
+ **File-scoped namespace declaration** [C#10]
```csharp
// 👎 non-compliant
namespace ApplicationA {
    class User {
        ...
    }
}
    
// 👍 preference
namespace ApplicationA;
class User {
    ...
}
```
    
+ **Namespace alias qualifier ```::```**
> ✔️ Pros: avoid conflict, abbreviate namespace
```csharp
// 📄 ApplicationA/User.cs
namespace ApplicationA;
class User {}

// 📄 ApplicationB/User.cs
namespace ApplicationB;
class User {}

// 📄 Driver.cs
using A = ApplicationA;
using B = ApplicationB;

A::User = new();
B::User = new();
```
    
+ **Aliased generics ```using```**
```csharp
// 👎 longhand
Dictionary<string, Dictionary<string, List<string>>> User1 = new();
Dictionary<string, Dictionary<string, List<string>>> User2 = new();

// 👍 shorthand
using ASimpleName = Dictionary<string, Dictionary<string, List<string>>>;
ASimpleName User1 = new();
ASimpleName User2 = new();
```

+ **Global using** directive to use namespace in all files of the project [[C#10](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive#global-modifier)]
    
+ ~~Region directive ```#region```~~
> Reason: Regions are considered anti-patterns. They require more work which doesn’t increase the quality or readability of the code, reduce the number of bugs, and makes the code more complicated to refactor.

+ ~~Base type casting~~ => **```System.Convert```** 
> Pros: Convert class enables to convert between non-compatible types
```csharp
// 👉 given
string variable = "5.00"; 

// 👎 non-compliant
double varDouble = (double)variable; // error: InvalidCastException

// 👍 preference
double varDouble = System.Convert.ToDouble(variable); // no error
```

+ ~~Objest casting~~ => **```as```**
> ✔️ Pros: if non-comatible types, casting throws InvalidCastException while ```as``` return null  
> ❌ Cons: potential to get NullReferenceException later
```csharp
// 👎 non-compliant
User instance = (User) mobileUser;

// 👍 preference
User instance = mobileUser as User;
```
