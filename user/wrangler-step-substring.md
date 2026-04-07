<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Substring -->

##### Substring

**Substring** step returns specific number of characters from provided text starting with specified character position. First character has position of 0.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Start position**: required, starting position of the substring. First character in the string has position of 0, last character has position of `length($Input) - 1`. Negative start positions are not allowed. Start position greater than or equal to the length of the input is allowed.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Number of characters**: required, number of characters returned to copy from the input string. Value must be greater or equal to 0. Values longer than the remainder of the string from **Start position** are allowed.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Starting position | Number of characters | Output value | Description |
| --- | --- | --- | --- | --- |
| "INV-20230328" | 4 | 4 | "2023" | Returns 4 characters starting from the fifth one (character with index 4 is the fifth character). |
| "INV-20230328" | 4 | 20 | "20230328" | If **Number of characters** is longer than the rest of the input after **Start position**, only the available characters are returned. |
| "London" | 10 | 5 | "" *(empty string)* | **Start position** is after the end of the input, empty string is returned. |
| "INV-20230328" | 0 | 3 | "INV" | First three characters of the input. Same result as using [Left substring step](wrangler-step-left.md) with **Number of characters** set to 3. |
| "INV-20230328" | 4 | 8 | "20230328" | Simpler solution would be reached by using [Right substring step](wrangler-step-right.md) |
| *No value* | any | any | *No value* | *No value* input produces *No value* output. |
| *Error* | any | any | *Error* | *Error* input value leads to *Error* on output. |

###### Remarks

- If **Starting position** is greater than the length of the input text, empty string "" is returned.
- If **Starting position** is less than the length of the input text and the **Number of characters** exceeds the length of the remainder of the input, only characters up to the end of the input are returned (no padding is done).

###### See also

- [Left substring step](wrangler-step-left.md)
- [Right substring step](wrangler-step-right.md)
- [`substring`](../developer/string-functions-ctl2.md#substring) function in CTL
