<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Remove whitespaces -->

##### Remove whitespaces

**Remove whitespaces** step removes all whitespace (invisible) characters from text including leading and trailing whitespaces as well as any whitespace characters within the text.

###### Parameters

- **Input column**: required, a string column to remove the whitespaces from.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| "Text with spaces." | "Textwithspaces." | Any space in the string is removed. |
| "   Text with lots of whitespace characters.    " | "Textwithlotsofwhitespacecharacters." | Any space including leading and trailing spaces are removed. |
| "Text      with  a new line." | "Textwithanewline." | All whitespace characters are removed; including new lines and tabs. |
| "1 st" | "1st" | All spaces in a sentence or between words are removed. |

###### Remarks

- **Remove whitespaces** step only works with string columns.
- Removes variety of "invisible" spacing characters not just spaces:
  - Regular space
  - New line (both Windows and Linux type)
  - Tab
- To remove only leading and trailing whitespace characters, use [Trim step](wrangler-step-trim.md).

###### See also

- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
- [Remove accents step](wrangler-step-remove-accents.md)
- [Remove non-alphanumeric characters step](wrangler-step-remove-non-alphanumeric.md)
- [Remove non-ASCII characters step](wrangler-step-remove-non-ascii.md)
- [Remove non-numeric characters step](wrangler-step-remove-non-numeric.md)
- [Remove non-printable characters step](wrangler-step-remove-non-printable.md)
