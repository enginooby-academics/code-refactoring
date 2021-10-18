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
