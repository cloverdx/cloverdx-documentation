<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Left substring -->

##### Left substring

**Left substring** allows you to extract specific number of characters from the beginning of text (i.e., it extracts first characters).

###### Parameters

- **Input column**: required, a string column containing input text.
- **Number of characters**: number of characters to extract from the input string. The value must be greater than or equal to zero. You can use values greater than the length of the input string - the whole input will be returned in such case (no padding is done).
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Number of characters | Output value | Description |
| --- | --- | --- | --- |
| "INV-20230328" | 3 | "INV" | Extract first three characters to determine type of a document ("Invoice"). |
| "short" | 10 | "short" | Using higher number of characters than the length of the input returns the whole input value. |
| "INV-20230328" | 0 | "" | Setting number of characters to 0 returns an empty string. Note that empty string is not the same as *No value* (which is stored as `null`). |
| *No value* | 5 | *No value* | Returns *No value* when called on *No value* input. |
| *Error* | any | *Error* | Calling the step on a cell with *Error* will result in an *Error*. |

###### Remarks

- Calling the step on a *No value* string results in *No value*.
- If number of characters specified in the parameter is greater than the length of the input string, the whole input string is returned.
- Calling the step on a cell with *Error* will result in an *Error*.

###### See also

- [Right substring step](wrangler-step-right.md)
- [Substring step](wrangler-step-substring.md)
- [`left`](../developer/string-functions-ctl2.md#left) function in CTL.
