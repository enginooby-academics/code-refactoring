# R

### Declaration, Initialization & Assignment
+ ~```=```~ => **```<-```**
> Reason: ```=``` operator can be forbidden in some contexts
```r
# 👎 non-compliant
a = 1

# 👍 preference
a <- 1
```

+ Multiple assignments
```
// 👎 longhand
a <- 1
b <- 1
c <- 1

// 👍 shorthand
a <- b <- c <- 1
```
