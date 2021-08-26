# C#

## Preferences
+ Check for nullity using **is** & **is not** _[C#9]_
```
if (a == null && b != null)
// preference
if (a is null && b is not null)
```

## Shorthands
+ **Switch expressions** _[C#8]_
```
enum BankStatus {Open, Closed, VIPOnly};

static bool CheckIfCanWalkIntoBankSwitch(BankStatus status, bool isVip)
{
    bool result = false;

    switch(status)
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
```
// shorthand (w/ arrow function)
static bool CheckIfCanWalkIntoBank(BankStatus status, bool isVip) => status switch
{
    BankBranchStatus.Open => true, 
    BankBranchStatus.Closed => false, 
    BankBranchStatus.VIPCustomersOnly => isVip
};
