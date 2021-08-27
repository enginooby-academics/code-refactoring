# C#

## Preferences
+ Check for nullity using **is** & **is not** _[C#9]_
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

User user = new User {Name = "John", age = 18};
user.Name = "John Ritter"; // no error
user.Age = 20; // error! CS8852.
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
    }

    return result;
}

// shorthand (w/ arrow function)
static bool CheckIfCanWalkIntoBank(BankStatus bankStatus, bool isVip) => bankStatus switch
{
    BankBranchStatus.Open => true, 
    BankBranchStatus.Closed => false, 
    BankBranchStatus.VIPCustomersOnly => isVip
};
```
+ **Implicit typing (var)**: for long named type
```
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();
// shorthand
var instance = new AReallyReallyLooooongClass();
```
+ **Concise new (new())** *[C#9]* 
```
ExampleClass instance = new ExampleClass();
// shorthand
ExampleClass instance = new();
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
