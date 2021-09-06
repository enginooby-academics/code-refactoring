# Dart


### String
+ **String multiplication** ```"abc" * 3 // "abcabcabc"```



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

+ Implement **call()** in class to make it callable like a function
```
class PasswordValidator {
  bool call(String password) {
    return password.length > 10;
  }
}

final validator = PasswordValidator();
validator('admin123');
```



### Collections
+ Iterate through map using its ~~keys/values~~ => **entries** properties
> Reason: access entries in a null-safe way, hence less error-prone
```
// given
const users = <String, int>{
  'Jeff 1': 18,
  'Jeff 2': 21,
  'Jeff 3': 17,
};

for (var name in users.keys) {
  final age = users[name]!;
  print('$name: $age');
}

// preference
for (var user in users.entries) {
  print('${user.key}: ${user.value}');
}
```
