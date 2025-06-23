### Variable syntax:
```VB
Dim <varname> As <datatype>
Const <constname> As <datatype>
```

### Pop-up syntaxes:
```VB
MsgBox <message>
```
```VB
InputBox(<message>, <window title>)

```

### Switch syntax:
```VB
Select Case <value>
Case <condition>
	...
Case <condition>
	...
Case Else
	...
End Select
```

### If syntax:
```VB
If <condition> Then
	...
ElseIf <condition> Then
	...
Else
	...
End If
```

### Loop syntaxes:
```VB
Do While <condition>
	...
Loop
```
```VB
Do
	...
Loop While <condition>
```
```VB
Do
	...
Loop Until <condition>
```
```VB
For <varname> = <startval> To <endval> Step <increment>
	...
Next <varname> 'Variable to be incremented by the previously specified amount
```
```VB
For Each <element> In <collection>
	...
Next
```

### Breaks and navigation syntax:
```VB
Exit For 'Break out of For loop
Exit Do 'Break out of Do loop
Exit Sub 'Prematurely break out of code block

On Error GoTo <label>
GoTo <label>
<label>:
Resume Next 'Return to line of code after error
```

### Value Conversion:
```VB
CInt(<value>) 'Returns integer
CStr(<value>) 'Returns string
CDbl(<value>) 'Returns double
LCase(<value>)
UCase(<value>)
Len(<value>)
Replace(<string>, <find>, <replacewith>)
```

### Other methods:
*in this case `<listbox>` can be replaced with a combo box*
```VB
<element>.SetFocus 'To access many properties, a control must have the focus
IsNumeric(<value>) 'Returns boolean indicate whether the argument is numeric
<listbox>.Column(<col>, <row>) 'Col and row begin at 0
DLookup(<field>, <fieldlocation>, <criteria>) 'Get value from a field from a record
Call
	<any parameter-less function>
	ClearAll(Me) 'Clears all textboxes in form
	ClearTextBox(<textbox>) 'Clears contents of a specific textbox
DoCmd
	.OpenForm

<listbox>.RowSource = <SQLcode>
<listbox>.ItemsSelected 'Returns a collection of selected items in a listbox
<listbox>.ItemData(<listentry>) 'Returns value of the specified entry in a list
```

### Operators:
```VB
= 'Equality
<> 'Reverse equality
> 'Greater than
< 'Less than
>= 'Greater than or equal to
<= 'Less than or equal to
AND
OR
NOT
XOR
+ 'Add numeric values
& 'Concatenate values
& _ 'Concatenate multi-line strings (mandatory space)
```

### Function definition:
```VB
Public Function <funcname>(<parametername> As <datatype>) As <returndatatype>
	...
	<funcname> = <returnval>
End Function
```