# C++

### Declaration, Initialization & Assignment
+ Use type **inference (auto)** [C+11]




### Collection
+ ~~Iterator~~ => **range based for loop** to iterate through arrays, vectocs [C++11]
```
vector<int> vec = {0, 1, 2, 3};

for (auto& value = vec.begin(); value != vec.end(); value++)
  cout << value << ' ';

//preference
for (const auto &value : vec)
  cout << value << ' ';
```

### OOP
+ **Initializer list** for constructor [[Reference](https://www.educative.io/edpresso/what-are-initializer-lists-in-cpp)]
> Pros: shorthand, init reference/constant members
```
class Point {
  private:
    int x;
    int y;
  public:
    //constructor
    Point(int i = 0, int j = 0) {
      x = i;
      y = j;
    }
    
    //preference
    Point(int i = 0, int j = 0) : x(i), y(j) {}
};
```
