<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Absolute value -->

##### Absolute value

Returns the absolute value of a given input. Absolute value is the number without its sign - i.e. always positive or zero.

###### Parameters

- **Input column**: required, a numeric column (decimal or integer).
- **Target column**: required, configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 5 | 5 |  |
| -5 | 5 |  |
| 10.5 | 10.5 |  |
| -10.5 | 10.5 |  |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [`abs`](../developer/mathematical-functions-ctl2.md#abs) function in CTL.
