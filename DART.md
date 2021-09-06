# Dart


### String
+ **String multiplication** ```"abc"*3 // "abcabcabc"```



### Async
+ Use **Future.wait** to execute multiple independent Futures concurrently
```
// Mock API class
class CovidAPI {
  Future<int> getCases() => Future.value(1000);
  Future<int> getRecovered() => Future.value(100);
  Future<int> getDeaths() => Future.value(10);
}

final api = CovidAPI();
final values = await Future.wait([
    api.getCases(),
    api.getRecovered(),
    api.getDeaths(),
]);
print(values); // [1000, 100, 10]
```


### OOP
+ Implement multiple inheritance using **mixin**
> Pros: reuse functions and attributes for different types
