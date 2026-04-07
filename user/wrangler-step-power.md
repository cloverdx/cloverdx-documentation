<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Raise number to a power -->

##### Raise number to a power

The **Raise number to a power** step computes the value of a number raised to a power. It allows you to compute value of *xy* where *x* comes from your data set and *y* is a fixed (constant) value you provide as a parameter.

###### Parameters

- **Input column**: a numeric column (decimal or integer) - the base of the power.
- **Power**: required, the exponent to which the base is raised. You can use integers as well as decimals (including fractions).
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Power | Output value | Description |
| --- | --- | --- | --- |
| 2 | 2 | 4 | *22 = 4* |
| 2 | 2.5 | 5.6568542494 | *22.5 = 5.6568542494* |
| -2 | 2.5 | *Error* | Raising negative numbers to fractional powers is not defined. |
| 2 | 0.5 | 1.4142…​ | *2 0.5 = 1.4142…​* |
| *No value* | *Any power* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [Exponential step](wrangler-step-exponential.md)
- [Common logarithm step](wrangler-step-common-log.md)
- [Natural logarithm step](wrangler-step-natural-log.md)
- [`pow`](../developer/mathematical-functions-ctl2.md#pow) function in CTL.
