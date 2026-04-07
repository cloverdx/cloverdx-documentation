<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Remove non-ASCII characters -->

##### Remove non-ASCII characters

**Remove non-ASCII characters** removes all characters that are not in US ASCII encoding.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. Output will always be of string type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| Voyez le brick géant que j’examine. | Voyez le brick gant que j’examine | Only the "é" is a non-US ASCII character therefore it was removed |
| Příšerný žluťoučký kůň úpěl ďábelské ódy. | Pern luouk k pl belsk dy. | This string has many non-US ASCII characters therefore many parts were removed |
| おはよう日本。 | "" (empty string) | Japanese text does not contain any ASCII characters and is completely removed. |
| *No value* | *No value* | Calling the step on *No value* returns *No value*. |
| *Error* | *Error* | Calling the step on *Error* returns *Error*. |

###### Remarks

- Calling the step on *No value* returns *No value*.
- Calling the step on cell with an *Error* returns *Error*.

###### See also

- [Remove accents step](wrangler-step-remove-accents.md)
- [Remove non-alphanumeric characters step](wrangler-step-remove-non-alphanumeric.md)
- [Remove non-numeric characters step](wrangler-step-remove-non-numeric.md)
- [Remove non-printable characters step](wrangler-step-remove-non-printable.md)
- [Remove whitespaces step](wrangler-step-remove-whitespaces.md)
- [Normalize whitespaces step](wrangler-step-normalize-whitespaces.md)
- [`removeNonAscii`](../developer/string-functions-ctl2.md#removenonascii) function in CTL.
