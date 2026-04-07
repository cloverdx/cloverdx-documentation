<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Remove non-numeric characters -->

##### Remove non-numeric characters

**Remove non-numeric characters** removes all characters except for (0-9) or decimal point (period character).

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 6.125% | 6.125 | Only characters 0-9 and decimal point are kept, % character is removed. |
| 123 2nd Street apartment 3b | 12323 | All of the whitespaces and alphabetical characters are removed. |
| *No value* | *No value* | Calling the step on *No value* returns *No value*. |
| *Error* | *Error* | Calling the step on *Error* returns *Error*. |

###### Remarks

- Calling the step on *No value* returns *No value*.
- Calling the step on cell with an *Error* returns *Error*.

###### See also

- [Remove accents step](wrangler-step-remove-non-numeric.md)
- [Remove non-alphanumeric characters step](wrangler-step-remove-non-alphanumeric.md)
- [Remove non-ASCII characters step](wrangler-step-remove-non-ascii.md)
- [Remove non-printable characters step](wrangler-step-remove-non-printable.md)
- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
