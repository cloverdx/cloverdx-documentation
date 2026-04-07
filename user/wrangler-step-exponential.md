<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Exponential -->

##### Exponential

The **Exponential** step performs the exponential function (*f(x) = ex*) on the values in the selected input column. Constant *e* is approximately 2.7182818285 and is the base of the natural logarithm.

###### Parameters

- **Input column**: required, a numeric column (decimal or integer).
- **Target column**: required, configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Output value | Description |
| --- | --- | --- |
| -2 | 0.13533…​ | *e-2 = 0.13533…​*. The larger a negative number in a column is, the closer the exponential function value is to 0. |
| 0 | 1 | *e0 = 1* |
| 1 | 2.7182818284 | *e1 = 2.7182818284 = e* |
| 51 | *Error* | *e44 = 1.409 x 1022* which is too large to fit into a decimal column. |
| *No value* | *Error* | *No value* input results in an error. |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.
- *Exponential* cannot be applied to values larger than *ln(max_decimal) = 50.6568720458*. Larger input values will result in an error since the output value is too large to be stored in a decimal column.

###### See also

- [Natural logarithm step](wrangler-step-natural-log.md)
- [`exp`](../developer/mathematical-functions-ctl2.md#exp) function in CTL.
