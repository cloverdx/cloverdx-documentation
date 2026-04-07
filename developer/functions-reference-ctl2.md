<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference -->

## 34. CTL2 functions reference

**CloverDX** transformation language has at its disposal a set of functions you can use. We describe them here.

All functions can be grouped into following categories:

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
> [!IMPORTANT]
> Remember that with CTL2 you can use both **CloverDX** built-in functions and your own functions in one of the ways listed below.
>
> **Built-in functions**
>
> - `substring(upperCase(getAplhanumericChars($in.0.field1))1,3)`
> - `$in.0.field1.getAlphanumericChars().upperCase().substring(1,3)`
>
> The two expressions above are equivalent. The second option with the first argument preceding the function itself is sometimes referred to as **object notation**. Do not forget to use the `$port.field.function()` syntax. Thus, `arg.substring(1,3)` is equal to `substring(arg,1,3).`
>
> You can also declare your own function with a set of arguments of any data type, e.g.:
>
>
> ```ctl
> function integer myFunction(integer arg1, string arg2, boolean arg3) {
>     <function body>
> }
> ```
>
>
> **User-defined functions**
>
> - `myFunction($in.0.integerField,$in.0.stringField,$in.0.booleanField)`
> - `$in.0.integerField.myFunction($in.0.stringField,$in.0.booleanField)`
> [!WARNING]
> Remember that the object notation (<first argument>.function(<other arguments>) cannot be used in **Miscellaneous** functions. See [Miscellaneous Functions](miscellaneous-functions-ctl2.md).
> [!IMPORTANT]
> Remember that if you set the **Null value** property in metadata for any `string` data field to any non-empty string, any function that accepts `string` data field as an argument and throws NPE when applied on `null` (e.g., `length()`) will throw NPE when applied on such specific string.
>
> For example, if `field1` has the **Null value** property set to `"<null>"`, `length($in.0.field1)` will fail on the records in which the value of `field1` is `"<null>"` and it will be 0 for empty field.
>
> For detailed information, see [Null value](metadata-editor.md#null-value-bridge).
