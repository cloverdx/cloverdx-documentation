<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Uppercase -->

##### Uppercase

**Uppercase** step converts all letter characters to uppercase form (i.e., it capitalizes all letters in the input).

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| "cloverdx" | "CLOVERDX" | All lowercase letters are transformed to uppercase. |
| "camelCase" | "CAMELCASE" | All lowercase letters are transformed to uppercase. |
| "Corporation Inc."" | "CORPORATION INC." | All lowercase letters are transformed to uppercase. |
| "inv07282710ph"" | "INV0728271PH" | All lowercase letters are transformed to uppercase while numerical characters stay the same. |
| *No value* | *No value* | Returns *No value* when called on *No value* input. |
| *Error* | *Error* | Calling the step on a cell with *Error* will result in an *Error*. |

###### Remarks

- Non-letter characters (e.g., digits, symbols, …​) remain without any changes.

###### See also

- [Lowercase step](wrangler-step-lowercase.md)
- [Propercase step](wrangler-step-propercase.md)
- [`upperCase`](../developer/string-functions-ctl2.md#uppercase) function in CTL.
