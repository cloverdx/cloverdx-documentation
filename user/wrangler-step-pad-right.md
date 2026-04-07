<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Pad right -->

##### Pad right

**Pad right** allows you to pad string values to specified minimum length by adding a designated character at the end of the string. If the input is longer than specified length, no change is made.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Length**: a numeric value containing minimal length of an output string. The value must be greater than 0.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Padding char**: required, a character used as a filler character. Only a single character can be used here.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Length | Padding char | Output value | Description |
| --- | --- | --- | --- | --- |
| "1234" | 8 | " " *(space)* | "1234    " | Pad to 8 characters by adding spaces at the end. |
| "1234" | 2 | "0" | "1234" | **Length** value is smaller than the length of the **Input value**, no change to input is made. |
| "1234" | 6 | "00" | *Error* | Padding character cannot contain multiple characters. |
| *No value* | any | any | *No value* | Calling the step on *No value* input will return *No value*. |
| *Error* | any | any | *Error* | Calling the step on an *Error* will return an *Error*. |

###### Remarks

- **Padding char** must contain exactly one character (including whitespace characters). Longer padding string will result in an error.
- If length of the input is longer than the specified **Length**, the input is returned unchanged.

###### See also

- [Pad left step](wrangler-step-pad-left.md).
- [`rpad`](../developer/string-functions-ctl2.md#rpad) function in CTL.
