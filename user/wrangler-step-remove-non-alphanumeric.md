<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Remove non-alphanumeric characters -->

##### Remove non-alphanumeric characters

**Remove non-alphanumeric characters** removes whitespaces, punctuation, math operators and other special characters from the text, only letters and numbers are kept.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| (8+4)*2 | 842 | The math operators (), +, and * are removed. |
| 34% of books | 34ofbooks | The math operator % is removed along with whitespaces. |
| gâteau | gâteau | All text is alphanumeric so it is unmodified. |
| おはよう日本。 | おはよう日本 | Japanese characters are not letters but are considered alpha-numeric and are not removed. The period character at the end is removed. |
| *No value* | *No value* | Calling the step on *No value* returns *No value*. |
| *Error* | *Error* | Calling the step on *Error* returns *Error*. |

###### Remarks

- Calling the step on *No value* returns *No value*.
- Calling the step on cell with an *Error* returns *Error*.

###### See also

- [Remove accents step](wrangler-step-remove-accents.md)
- [Remove non-ASCII characters step](wrangler-step-remove-non-ascii.md)
- [Remove non-numeric characters step](wrangler-step-remove-non-numeric.md)
- [Remove non-printable characters step](wrangler-step-remove-non-printable.md)
- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
