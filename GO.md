# Go

### Declaration, Initialization & Assignment
+ Init successive integer constants using **{iota}** [[Reference](https://yourbasic.org/golang/iota/)]
```go
const (
  C1 = iota + 1 // offset 1
  _ // skip
  C3
  C4
)

fmt.Println(C1, C3, C4) // "1 3 4"
```