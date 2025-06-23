# Bitwise Operators
## Review
We can operate on any byte. So for instance, given
```c
short sValue = 0x1234;
char* cPtr = &sValue;
```

We could print out
```c
printf("%x\n", sValue); // Prints 1234 (hex)
printf("%d\n", sValue); // Prints 4660 (decimal)
printf("%x\t%d\n", *cPtr, *cPtr); // Prints 34 (hex) and 52 (decimal) 
printf("%x\t%d\n", *(cPtr + 1), *(cPtr + 1)); // Prints 12 (hex) and 18 (decimal)
```

### Operating on the bit level
Since the OS is byte-addressable we need bitwise operators

| Bitwise |       |       | `~var1`   | `a & b`     | a \| b     | a ^ b       |
| ------- | ----- | ----- | --------- | ----------- | ---------- | ----------- |
| Logical |       |       | `!a`      | `a && b`    | a \|\| b   |             |
| Boolean | **a** | **b** | **NOT a** | **a AND b** | **a OR b** | **a XOR b** |
|         | 0     | 0     | 1         | 0           | 0          | 0           |
|         | 0     | 1     | 1         | 0           | 1          | 1           |
|         | 1     | 0     | 0         | 0           | 1          | 1           |
|         | 1     | 1     | 0         | 1           | 1          | 0           |
- Using `0` for false and `1` for true
- Bitwise operators work on **all** bits of the variables operated on
- So if `var1 = 0x12=`**`0b0001'0010`**, then **`~`**`var1 = 0b1110'1101 = 0xED`
- If `var1 = 0x12` and `var2 = 0x34 =` **`0b0011'0100`**, then `var1`**`&`**`var2 =`**`0b0001'0000`**`= 0x10`
- If `var1 = 0x12` and `var2 = 0x34`, then `var1`**`|`**`var2 =`**`0b0011'0110`** `= 0x36`
- if `var1 = 0x12` and `var2 = 0x34`, then `var1`**`^`**`var2 =`**`0b0010'0110`**
