#Use of unsigned ints

> Using an unsigned instead of an int to gain one more bit to represent positive integers is almost never a good idea

\- Bjarne Stroustrup

Casting signed to unsigned and vice-versa results in daemons because values that are not represented in 1 will be converted to an opposite extreme in the other - the wrap around.

For example

```
    unsigned u = INT_MAX;
    // 2147483647
    // 01111111111111111111111111111111

    int i2 = (u+1;
    // -2147483648
    // 10000000000000000000000000000000
```


### Rule of thumb

Unless you need some large value outside the range of a signed representation, use the signed representation.
