<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Ceiling -->

##### Ceiling

**Ceiling** step rounds the number up to the nearest integer. Negative numbers are rounded towards zero while positive numbers are rounded away from zero.

###### Parameters

- **Input column**: a decimal column.
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 2.1 | 3 | Positive numbers are rounded away from zero. |
| -2.9 | -2 | Negative numbers are rounded towards zero. |
| *No value* | *Error* | Calling **Ceiling** on an empty value results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [Floor step](wrangler-step-floor.md) to round numbers down to the nearest integer.
- [Round step](wrangler-step-round.md) to round numbers to provided number of decimal places.
- [Truncate step](wrangler-step-truncate.md) to remove decimal portion of a number.
- [`ceil`](../developer/mathematical-functions-ctl2.md#ceil) function in CTL.
