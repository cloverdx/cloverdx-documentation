<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Square root -->

##### Square root

Returns the square root of a positive numerical input (decimal or integer) as a positive decimal or integer.

###### Parameters

- **Input column**: a numeric column (decimal or integer).
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 4 | 2 |  |
| -4 | *Error* | No square root for a negative number. |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Square root of a negative number is a complex number which cannot be stored in decimal. Calling **Square root** on negative numbers will result in an error.
- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See Also

- [`sqrt`](../developer/mathematical-functions-ctl2.md#sqrt) function in CTL.
