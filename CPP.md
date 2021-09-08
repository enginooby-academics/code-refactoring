# C++

### Declaration, Initialization & Assignment
+ Use **type inference ```auto```** [C++11]
```cpp
// 👎 non-compliant
char name[] = "John";
int age = 18;

// 👍 preference
auto name[] = "John";
auto age = 18;
```

+ Alias type using **```typedef```**
```cpp
typedef long long ll;
ll a = 123LL;
```

+ Use **initializer list** to init containers [C++11] 
```cpp
// 👎 longhand
pair<int, int> p = make_pair(3, 4);

// 👍 shorthand
pair<int, int> p = {3, 4};
vector<int> v = {1, 2, 5, 2};
set<int> s = {4, 6, 2, 7, 4};
```

### Collection (Container)
+ ~~Iterator~~ => **range-based for loop** to iterate through arrays, vectocs, string [C++11]
```cpp
// 👉 given
vector<int> vec = {0, 1, 2, 3};

// 👎 non-compliant
for (set<int>::iterator it = s.begin(); it != s.end(); ++it)
  cout << *it << ' ';

// 👍 preference
for (const auto &value : vec)
  cout << value << ' ';
```

+ **Inbuilt functions**
```cpp
// are all of the elements positive?
all_of(first, first+n, ispositive()); 

// is there at least one positive element?
any_of(first, first+n, ispositive());

// are none of the elements positive?
none_of(first, first+n, ispositive()); 
```




### OOP
+ **Initializer list** for constructor [[Reference](https://www.educative.io/edpresso/what-are-initializer-lists-in-cpp)]
> Pros: shorthand, init reference/constant members
```cpp
class Point {
  private:
    int x;
    int y;
  public:
    // 👎 non-compliant
    Point(int i = 0, int j = 0) {
      x = i;
      y = j;
    }
    
    // 👍 preference
    Point(int i = 0, int j = 0) : x(i), y(j) {}
};
```



### String
+ ~~strlen()~~
```cpp
// 👎 non-compliant
for (int i = 0; i < strlen(s); ++i)

// 👍 preference
for (int i = 0; s[i]; ++i)
```

+ ~~```endl```~~ => **```/n```**
> Pros: faster [?]


### Number
+ **Inbuilt functions**
```cpp
#include <numeric>
std::gcd(p, q) // get greatest common divisor [C++17]
```
