<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Remove non-printable characters -->

##### Remove non-printable characters

**Remove non-printable characters** removes all non-printable characters from value - tabs, line breaks, page breaks and variety of control characters. Note that regular spaces as used between words are not removed.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| Welcome:⟶John    Doe! | Welcome:John Doe! | The tab (denoted by the ⟶ symbol in the example) is removed while the four regular spaces between words are kept. |
| Please sign here:   John Doe | Please sign here:John Doe | The spaces are kept while new line characters are removed. |
| *No value* | *No value* | Calling the step on *No value* returns *No value*. |
| *Error* | *Error* | Calling the step on *Error* returns *Error*. |

###### Remarks

- **Remove non-printable characters** removes all non-printable characters. you can find a full list [here](https://www.fileformat.info/info/unicode/category/Cc/list.htm).
- Calling the step on *No value* returns *No value*.
- Calling the step on cell with an *Error* returns *Error*.

###### See also

- [Remove accents step](wrangler-step-remove-accents.md)
- [Remove non-alphanumeric step](wrangler-step-remove-non-alphanumeric.md)
- [Remove non-ASCII step](wrangler-step-remove-non-ascii.md)
- [Remove non-numeric step](wrangler-step-remove-non-numeric.md)
- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
- [`removeNonPrintable`](../developer/string-functions-ctl2.md#removenonprintable) function in CTL.
