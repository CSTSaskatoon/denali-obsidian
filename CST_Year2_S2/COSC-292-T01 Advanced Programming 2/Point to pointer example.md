```c
void main()
{
    const char* name = "Banana";
    const char charToFind = 'n';
    char* wrongLastOccurancePtr = NULL;
    char* correctLastOccurancePtr = NULL;

    wrong(name, charToFind, lastOccurancePtr);
    correct(name, charToFind, &correctLastOccurancePtr);

    printf("wrongLastOccurancePtr is %c\n", *wrongLastOccurancePtr); // NULL
    printf("correctLastOccurancePtr is %c\n", *correctLastOccurancePtr); // n (specifically the last n in name
    printf("correctLastOccurancePtr as a string is %s\n", correctLastOccurancePtr); // na (because it is referencing the last n of Banana in memory
}

void wrong(const char* name, const char charToFind, char* lastOccurancePtr)
{
    for (int i = 0; i < strlen(name); i++)
    {
        if (name[i] == charToFind)
        {
            lastOccurancePtr = name + i;
        }
    }
    // This will work here, but since lastOccurancePtr is  not the same as wrongLastOccurancePtr
    // in main, this DOES NOT WORK IN MAIN. lastOccurancePtr is a COPY of wrongLastOccurancePtr
    printf("lastOccurancePtr is %c\n", *lastOccurancePtr);
}

void correct(const char* name, const char charToFind, char** PtrToLastOccurancePtr)
{
    for (int i = 0; i < strlen(name); i++)
    {
        if (name[i] == charToFind)
        {
            *PtrToLastOccurancePtr = name + i;
        }
    }
    // This will work here AND IN MAIN, because *lastOccurrancePtr is referencing correctLastOccurancePtr
    // in main instead of being a copy of correctLastOccurancePtr
    printf("lastOccurancePtr is %c\n", **PtrToLastOccurancePtr);
}
```

### Big Endian vs Little Endian
`int example = 0x87654321`

| Memory Address | Alias   | Byte's value in little Endian | Byte's value in big Endian |
| -------------- | ------- | ----------------------------- | -------------------------- |
| 0x0000000D     |         |                               |                            |
| 0x0000000C     |         |                               |                            |
| 0x0000000B     |         |                               |                            |
| 0x0000000A     |         |                               |                            |
| 0x00000009     |         |                               |                            |
| 0x00000008     |         |                               |                            |
| 0x00000007     |         |                               |                            |
| 0x00000006     |         |                               |                            |
| 0x00000005     |         |                               |                            |
| 0x00000004     |         | 0x87                          | 0x21                       |
| 0x00000003     |         | 0x65                          | 0x34                       |
| 0x00000002     |         | 0x34                          | 0x65                       |
| 0x00000001     | example | 0x21                          | 0x87                       |
