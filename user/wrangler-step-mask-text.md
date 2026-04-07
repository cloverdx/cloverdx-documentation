<!-- End user’s guide > Wrangler user guide > Transformation steps > Data anonymization steps > Mask text -->

##### Mask text

**Mask text** step implements data masking algorithms that allow you to hide private data in simple way. For example, you can use it to mask out parts of phone numbers, credit cards, personal names, and so on.

###### Parameters

- **Input column**: required, a string column containing input text to mask.
- **Characters to mask**: required, determines what kind of characters to mask. Following options are available:
  - **Letters and digits**: default, only mask letters and digits, whitespaces and other characters will remain as they were.
  - **Letters only**: only mask letters, all other characters will remain as they were.
  - **Digits only**: only mask digits, all other characters will remain as they were.
  - **All characters**: mask all characters regardless of their type (this is the most generic option).
- **Masking character**: required, a single character that will be used as a replacement for each character selected in the *Characters to mask* parameter.
- **Mask suffix**: configure how many characters from the input value to mask in each group of characters of the same type. Value must be an integer greater than or equal to 0. Two options are available:
  - **All**: all characters are considered for masking.
  - **Number of characters from a string group to preserve unmasked**: allows you to specify the number of characters from the beginning of each group of characters that will not be masked. Value must be at least 1.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Characters to mask | Masking character | Mask suffix | Result | Description |
| --- | --- | --- | --- | --- | --- |
| "123-456-7890" | Digits only | "x" | All | "xxx-xxx-xxxx" | Mask all digits in each group. |
| "123-456-7890" | Letters only | "x" | All | "123-456-7890" | No change - input value does not contain any letters. |
| "123-456-7890" | All | "x" | All | "xxxxxxxxxxxx" | Mask all characters - the result will be the same length as input and will consist entirely of the mask characters. |
| "123-456-7890" | Digits only | "x" | 2 | "12x-45x-78xx" | Find all digits and from each group of digits keep the first two (based on prefix length) and replace the remaining digits with "x". |
| "" (empty string) | Any | Any | Any | "" (empty string) | Calling the step on an empty string will return empty string. |
| *No value* | Any | Any | Any | *No value* | Calling the step on *No value* input will return *No value*. |
| *Error* | Any | Any | Any | *Error* | Calling the step on an *Error* will return an *Error*. |

###### Remarks

- Calling the step on a *No value* string results in *No value*.
- Calling the step on a cell with *Error* will result in an *Error*.

###### See also

- [Replace text step](wrangler-step-replace-text.md)
- [Add noise to number](wrangler-step-add-noise-to-number.md)
- [Add noise to date](wrangler-step-add-noise-to-date.md)
- [`replace`](../developer/string-functions-ctl2.md#replace) function in CTL.
- [`addNoise`](../developer/mathematical-functions-ctl2.md#addnoise) function.
