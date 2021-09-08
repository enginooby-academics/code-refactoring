# Dart


### String
+ **String multiplication** ```"abc" * 3 // "abcabcabc"```
+ ~~Escape sequence~~ => **raw string ```r```**
```dart
// 👎 non-compliant
string myFile = "C:\\myfolder\\myfile.txt";

// 👍 preference
string myFile = r'C:\myfolder\myfile.txt';
```



### Function
+ Use underscores for unused arguments
> Reason: more compact, avoid paying attention on unnecessary details
```dart
// 👎 non-compliant
ListView.builder(
  itemBuilder: (context, index) => ListTile(
    title: Text('all the same'),
  ),
  itemCount: 10,
);

// 👍 preference
ListView.builder(
  itemBuilder: (_, __) => ListTile( // _ is different than __
    title: Text('all the same'),
  ),
  itemCount: 10,
);
```

+ Use **cascade operator ```..```** to perform a sequence of operations on the same object
```dart
// 👎 non-compliant
user.setName("Jeff");
user.setAge(18);
user.showInfo();

// 👍 preference
user..setName("Jeff") 
    ..setAge(18)
    ..showInfo(); 
```


### Async
+ Use **```Future.wait```** to execute multiple independent Futures concurrently
```dart
// 👉 given: mock API class
class CovidAPI {
  Future<int> getCases() => Future.value(1000);
  Future<int> getRecovered() => Future.value(100);
  Future<int> getDeaths() => Future.value(10);
}

final api = CovidAPI();

// 👍 preference
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

+ Implement **```call()```** in class to make it callable like a function
```dart
class PasswordValidator {
  bool call(String password) {
    return password.length > 10;
  }
}

final validator = PasswordValidator();
validator('admin123');
```

+ Auto-generate hashCode, == and toString() implementations using **Equatable** package


### Collections
+ Iterate through map using its ~~keys/values~~ => **```entries```** properties
> Reason: access entries in a null-safe way, hence less error-prone
```dart
// 👉 given
const users = <String, int>{
  'Jeff 1': 18,
  'Jeff 2': 21,
  'Jeff 3': 17,
};

// 👎 non-compliant
for (var name in users.keys) {
  final age = users[name]!;
  print('$name: $age');
}

// 👍 preference
for (var user in users.entries) {
  print('${user.key}: ${user.value}');
}
```
