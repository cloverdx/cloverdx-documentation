<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Truncate -->

##### Truncate

**Truncate** step removes decimal portion of a number and converts it to an integer.

###### Parameters

- **Input column**: required, a decimal column to truncate.
- **Target column**: requried, configure the column which will receive the output. Output will always be of integer type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 1.2 | 1 | Decimal portion is removed. |
| 2.9 | 2 | Decimal portion is removed. Note that **Truncate** step does not round decimal numbers, it just removes the decimal part of it. |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [Ceiling step](wrangler-step-ceiling.md) to round numbers up to the nearest integer.
- [Floor step](wrangler-step-floor.md) to round numbers down to the nearest integer.
- [Round step](wrangler-step-round.md) to round numbers to provided number of decimal places.
- [`decimal2long`](../developer/conversion-functions-ctl2.md#decimal2long) CTL function.
