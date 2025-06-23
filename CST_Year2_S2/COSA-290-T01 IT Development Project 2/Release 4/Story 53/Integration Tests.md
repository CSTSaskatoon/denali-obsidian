### Registration Page
```
Expected: exactly one matching candidate
  Actual: _TextWidgetFinder:<Found 0 widgets with text "Last name
is required": []>
   Which: means none were found but one was expected
367:7

Expected: exactly one matching candidate
  Actual: _TextWidgetFinder:<Found 0 widgets with text "First
name is required": []>
   Which: means none were found but one was expected
437:7

Expected: exactly one matching candidate
  Actual: _TypeWidgetFinder:<Found 0 widgets with type
"SnackBar": []>
   Which: means none were found but one was expected
932:7

The finder "Found 0 widgets with text "Profile": []" (used in a
call to "tap()") could not find any matching widgets.
1017:19
```

### Evaluation page
```
The finder "Found 0 widgets with key [<'loginButton'>]: []" (used
in a call to "tap()") could not find any matching widgets.
26:18

^ This fails 5 times, one for every test
```

### Password Reset
```
Unexpected null value.
236:39

The finder "Found 0 widgets with text "Login as Owner": []" (used
in a call to "tap()") could not find any matching widgets.
320:17
```

**Doesn't always fail**

### Evaluation Tags
```
The finder "Found 0 widgets with key [<'loginButton'>]: []" (used
in a call to "tap()") could not find any matching widgets.
26:18

^ This fails 4 times, one for every test
```