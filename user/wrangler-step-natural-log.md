<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Natural logarithm -->

##### Natural logarithm

The **Natural logarithm** step computes the mathematical natural logarithm (*loge(x)* or sometimes also *ln(x)*) of the values in the selected input column.

###### Parameters

- **Input column**: a numeric column (decimal or integer).
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 1 | 0 |  |
| 1000000 | 13.8155105579 |  |
| -2 | *Error* | Natural logarithm is not defined for negative numbers and results in an error. |
| 0 | *Error* | Natural logarithm is not defined for 0 and results in an error. |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.
- **Natural logarithm** step can only be applied to values greater than 0. Natural logarithm is not defined for zero or negative values and will return an error.

###### See also

- [Exponential step](wrangler-step-exponential.md)
- [`log`](../developer/mathematical-functions-ctl2.md#log) function in CTL.
