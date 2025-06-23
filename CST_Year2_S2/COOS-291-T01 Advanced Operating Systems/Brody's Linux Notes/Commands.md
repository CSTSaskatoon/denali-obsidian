## Tree

```
sudo apt install tree
```

## Punctuation Syntax

---

| Name                          | Symbol  | Meaning                                                                                                         | Example | Result |
| ----------------------------- | ------- | --------------------------------------------------------------------------------------------------------------- | ------- | ------ |
| Variable                      | `$`     | Read a variable/reference                                                                                       |         |        |
| Brace Expansion               | `{}`    | Repeatedly do a command with all the parameters within the braces                                               |         |        |
| Arithmetic                    | `$(())` | Does integer math. Uses all values inside without need `$` on references, or `\` escape on expressions          |         |        |
| Weak Quote/Variable Expansion | `""`    | Read an argument and pulls the value(s) of references                                                           |         |        |
| String Qutoe                  | `''`    | Read all the exact values inside as typed                                                                       |         |        |
| Command Substitution          | `$()`   | This will do an operation inside and save the output. You can assign  variables to the result of that operation |         |        |
| Process Substitution          | `<()`   | Take output of command and put into a "file descriptor". Can be treated like pipes                              | ?       |        |
| Set                           | `:=`    | Set a variable to a new value                                                                                   |         |        |
| Default Set                   | `:-`    | Set a variable to a new value if that variable is not assigned/set                                              |         |        |
| Unset                         | `unset` | This keyword will make a variable null/unassigned                                                               |         |        |
| Match Close Left              | `#`     | Regex. Match will find the first pattern on the left, then stop when it finds the NEXT value/end of pattern     |         |        |
| Match Large Left              | `##`    | Regex. Match will find the first pattern on the left, then stop when it finds the LAST value/end of pattern     |         |        |
| Match Close Right             | `%`     | Same as Match Close Left, only it starts from the right                                                         |         |        |
| Match Large Left              | `%%`    | Same as Match Large Left, only it starts from the right                                                         |         |        |
### CHMOD

![[Pasted image 20250128161711.png]]

```
chmod <flags> <param>
```

[[Day 2 Terminal File Navigation and Permissions#Permissions|CHMOD in notes]]
