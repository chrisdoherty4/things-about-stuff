# Runes

A rune represents a unicode code point and is type alias to an int32. This shouldn't be confused with Utf-8 encoding where the rune could be reduced to a single byte.

For example, the letter 'A' is 65 (0x41) and is representable in Utf-8 as 1 byte but can also be represented as an integer. 

```
var codepoint rune
codepoint = 0x41

fmt.Println(string(codepoint))
// A
```
```
