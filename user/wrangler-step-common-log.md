<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Common logarithm -->

##### Common logarithm

The **Common logarithm** step computes the common logarithm of the input values (*log10(x) or sometimes also log(x)*). Common is a logarithm with base equal to 10.

###### Parameters

- **Input column**: a numeric column (decimal or integer).
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| 1 | 0 |  |
| 1000000 | 6 |  |
| -2 | *Error* | Common logarithm is not defined for negative numbers and results in an error. |
| 0 | *Error* | Common logarithm is not defined for 0 and results in an error. |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.
- **Common logarithm** step can only be applied to values greater than 0. Common logarithm is not defined for zero or negative values and will return an error.

###### See also

- [Power step](wrangler-step-power.md)
- [Natural logarithm step](wrangler-step-natural-log.md)
- [`log10`](../developer/mathematical-functions-ctl2.md#log10) function in CTL.
