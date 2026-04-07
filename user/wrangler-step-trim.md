<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Trim -->

##### Trim

**Trim** step removes leading and trailing spaces from text. Spaces within the text (i.e., spaces between words) are left without any changes.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| "Spaces after    " | "Spaces after" | Trailing spaces are removed. |
| "    Spaces before" | "Spaces before" | Leading spaces are removed. |
| "    Space before and after    " | "Space before and after" | Both leading and trailing spaces are removed. |
| "    Spaces    in    the    middle    " | "Spaces    in    the    middle" | Leading and trailing spaces are removed but spaces between words are left unchanged. |
| "    " (spaces only) | "" (empty text) | **Trim** of text containing only spaces results in empty text - a string with zero length. Note this is different than *No value*. |
| "" (empty text) | "" (empty text) | **Trim** of empty text produces empty text (zero-length string). Note this is different than *No value*. |
| *No value* | *No value* | **Trim** of a *No value* cell results in a *No value* output. |
| *Error* | *Error* | Running **Trim** on errors propagates error. |

###### Remarks

- **Trim** removes variety of whitespace characters not just "regular" spaces:
  - Space character (various variants of Unicode space characters are removed)
  - New line characters and their combinations as used in Windows, Mac or Linux (line feed `\n`, form feed `\f`, carriage return `\r`, line separator `\u2028`, paragramp separator `\u2029`)
  - Tab (both horizontal tab `\t` as well as vertical tab `\u000B`)
  - Unicode separator character (file, group, record, unit separators)
- Calling **Trim** step on a cell with *Error* will result in an *Error*.

###### See also

- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [`trim`](../developer/string-functions-ctl2.md#trim) function in CTL.
