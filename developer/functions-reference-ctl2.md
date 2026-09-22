<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference -->

## 36. CTL2 functions reference

CloverDX Transformation Language (CTL) provides a comprehensive library of built-in functions for common data transformation and processing tasks.

The built-in functions are organized into the following categories:

- [Conversion functions](conversion-functions-ctl2.md)
- [Container functions](container-functions-ctl2.md)
- [Record functions (dynamic field access)](field-access-functions-ctl2.md)
- [Date functions](date-functions-ctl2.md)
- [Mathematical functions](mathematical-functions-ctl2.md)
- [String functions](string-functions-ctl2.md)
- [Mapping functions](mapping-functions-ctl2.md)
- [Miscellaneous functions](miscellaneous-functions-ctl2.md)
- [Lookup table functions](lookup-table-functions-ctl2.md)
- [Sequence functions](sequence-functions-ctl2.md)
- [Subgraph functions](subgraph-functions-ctl2.md)
- [Data Service HTTP Library functions](http-ctl2.html)
- [Custom CTL functions](custom-functions-ctl2.md)

Besides built-in functions, CTL2 also lets you declare your own functions. You can declare your own functions with arguments of supported data types. For example:

```ctl
function integer myFunction(integer arg1, string arg2, boolean arg3) {
    <function body>
}
```

Both built-in and custom functions can be called using either standard notation or object notation.

In standard notation, the function is followed by its arguments in parentheses. For example:

```ctl
substring(upperCase(getAlphanumericChars($in.0.field1)), 1, 3)
myFunction($in.0.integerField, $in.0.stringField, $in.0.booleanField)
```

Alternatively, you can use **object notation**, where the first argument precedes the function:

```ctl
$in.0.field1.getAlphanumericChars().upperCase().substring(1, 3)
$in.0.integerField.myFunction($in.0.stringField, $in.0.booleanField)
```

The two expressions are equivalent.

For both notations, see [Calling a function](language-reference-ctl2.md#calling-a-function).
> [!WARNING]
> The object notation (`<first argument>.function(<other arguments>`) cannot be used in **Miscellaneous** functions. See [Miscellaneous Functions](miscellaneous-functions-ctl2.md).
> [!IMPORTANT]
> The **Null value** metadata property affects how functions handle string fields.
>
> If the Null value property of a string field is set to a non-empty string, a function that throws a `NullPointerException` when applied to null, such as `length()`, also throws the exception when applied to that configured null value.
>
> For example, suppose `field1` has its Null value property set to `"<null>"`. In that case:
>
>
> ```ctl
> length($in.0.field1)
> ```
>
>
> fails for records where the value of field1 is `"<null>"`. For an empty field, the function returns `0`.
>
> For more information, see [Null value](metadata-editor.md#null-value-bridge).
