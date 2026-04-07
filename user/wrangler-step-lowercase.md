<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Lowercase -->

##### Lowercase

**Lowercase** step converts all letter characters to their lowercase form.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| "CLOVERDX" | "cloverdx" | All uppercase letters are transformed to lowercase. |
| "camelCase" | "camelcase" | All uppercase letters are transformed to lowercase. |
| "Corporation Inc."" | "corporation inc." | All uppercase letters are transformed to lowercase. |
| "INV07282710PH"" | "inv0728271ph" | All uppercase letters are transformed to lowercase while numerical characters stay the same. |
| *No value* | *No value* | Returns *No value* when called on *No value* input. |
| *Error* | *Error* | Calling the step on a cell with *Error* will result in an *Error*. |

###### Remarks

- Non-letter characters (e.g., digits, symbols, …​) remain without any changes.

###### See also

- [Uppercase step](wrangler-step-uppercase.md)
- [Propercase step](wrangler-step-propercase.md)
- [`lowerCase`](../developer/string-functions-ctl2.md#lowercase) function in CTL.
