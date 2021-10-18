### Numeric
+ Use underscore *```_```* as digit separator in long numeric literals [[Java7](https://docs.oracle.com/javase/8/docs/technotes/guides/language/underscores-literals.html)]
```java
// 👎 non-compliant
long creditCardNumber = 1234567890123456L;
long hexBytes = 0xFFECDE5E;
long bytes = 0b11010010011010011001010010010010;

// 👍 preference
long creditCardNumber = 1234_5678_9012_3456L;
long hexBytes = 0xFF_EC_DE_5E;
long bytes = 0b11010010_01101001_10010100_10010010;
```

### Collection
+ Use ~~_**double-brace initialization/stream**_~~ => _**convenience factory method**_ to initialize collections [[Java9](https://www.baeldung.com/java-9-collections-factory-methods)]
```java
// 👎 traddictional: verbose 
Set<String> set = new HashSet<>();
set.add("one");
set.add("two");
set.add("three");
set = Collections.unmodifiableSet(set);

// 👎 double-brace initialization: reduces the readability, anti-pattern
Set<String> set = Collections.unmodifiableSet(new HashSet<String>() {{
  add("one"); add("two"); add("three");
}});

// 👎 stream: not obvious and intuitive, creates of unnecessary objects, can't create Map
Stream.of("one", "two", "three").collect(collectingAndThen(toSet(), Collections::unmodifiableSet));

// 👍 convenience factory
Set<String> set = Set.of("one", "two", "three");
```

