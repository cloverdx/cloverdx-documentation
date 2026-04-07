<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Normalize whitespaces -->

##### Normalize whitespaces

**Normalize whitespaces** step removes tabs, new line or carriage return characters, and extra spaces from the input text and replaces them with a single space character when in between words, or removes them completely when before the first word or after the last word. This step can help you optimize your data and quickly remove unwanted characters that were entered in error or that are in an unwanted format.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the **Input column** with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the **Input column**.

###### Examples

| Input value | Output value | Explanation |
| --- | --- | --- |
| "Text with single spaces." | "Text with single spaces." | No change because there are no extra whitespace characters. |
| "Text with    lots of    space     characters." | "Text with lots of space characters." | All extra spaces are removed. |
| "Text      with tabs and         a new line." | "Text with tabs and a new line." | All extra spaces, tabs, and new line/carriage return characters are removed. |
| " Test word " | "Test word" | Extra spaces at the beginning and end are removed. |
| *No value* | *No value* | Empty value produces empty value on output. |
| *Error* | *Error* | Applying the step to an error results in another *Error*. |

###### See also

- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [Remove accents step](wrangler-step-remove-accents.md)
- [Remove non-alphanumeric characters step](wrangler-step-remove-non-alphanumeric.md)
- [Remove non-ASCII characters step](wrangler-step-remove-non-ascii.md)
- [Remove non-numeric characters step](wrangler-step-remove-non-numeric.md)
- [Remove non-printable characters step](wrangler-step-remove-non-printable.md)
- [`normalizeWhitespaces`](../developer/string-functions-ctl2.md#normalizewhitespaces) function in CTL.
