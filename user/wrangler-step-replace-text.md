<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Replace text -->

##### Replace text

**Replace text** replaces all matches of a regular expression within text with the replacement text.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Replaced text**: required, a regular expression to search for in the input text. Note that the replace function is case-sensitive.
- **Replacement**: optional, text which will be used as replacement for each occurrence of the **Replaced text** in the input. If left empty, the value in the **Replaced text** field will be deleted.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Replaced text | Replacement | Result | Description |
| --- | --- | --- | --- | --- |
| Two boxes: red box and blue BOX | box | car | Two cares: red car and blue BOX | Simple replacements without special symbols can be done directly. Search for instances of "box" and replace with "car". Search is case-sensitive, so word "BOX" is left as is. |
| Hello, Emily. | `[Ee]` | `-X-` | H-X-llo, -X-mily | Square brackets define character group. Here we define a group that contains "E" and "e"All occurrences of letters from the group are replaced with string `-X-`. |
| Hello, Emily | e(l+) | a$1 | Hallo, Emily | In this example we define capture group using round brackets and use it to capture all lower-case Ls. The group is then referenced in the replacement text using `$1` syntax. |
| *No value* | *No value* | Calling the step on *No value* returns *No value*. | *Error* | *Error* |

###### Remarks

- Calling the step on *No value* returns *No value*.
- Calling the step on cell with an *Error* returns *Error*.

###### See also

- [`replace`](../developer/string-functions-ctl2.md#replace) function in CTL.
- [Regular expressions in CTL (CloverDX documentation)](../developer/language-reference-ctl2.md#regular-expressions)
- [Regular expressions (on Wikipedia)](https://en.wikipedia.org/wiki/Regular_expression)
- [Regular Expression Language - Quick Reference (on microsoft.com)](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference)
