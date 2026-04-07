<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Round -->

##### Round

Returns to the nearest whole (integer) number. Mathematical rounding is used - values ending in digit 5 will be rounded away from zero, values less than 5 will round towards zero.

###### Parameters

- **Input column**: a number to round, must be a decimal column.
- **Precision**: specifies the number of digits to round the input to.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
  - The precision behaves as follows:
    - *0*: round to whole numbers.
    - *Positive value*: round to specified number of decimal places.
    - *Negative value*: round to multiples of 10, 100, etc.
- **Target column**: configure the column which will receive the output. Output will always be of decimal type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Precision | Output value |
| --- | --- | --- |
| Description | 4.125 | 0 |
| 4 | Rounds to the nearest whole number. | -4.125 |
| 0 | -4 | Rounds to the nearest whole number. |
| 4.125 | 1 | 4.1 |
| Rounds to one decimal place. | -4.125 | 1 |
| -4.1 | Rounds to one decimal place. | 4.125 |
| 2 | 4.13 | Rounds to two decimal places. |
| -4.125 | 2 | -4.13 |
| Rounds to two decimal places. | 453.4 | -1 |
| 450 | Rounds to the nearest multiple of 10. | 453.4 |
| -2 | 500 | Rounds to the nearest multiple of 100. |
| `null` | (any) | Error |

###### Remarks

- Applying the step to *No value* cells (cells containing *null*) will result in an error.

###### See also

- [`round`](../developer/mathematical-functions-ctl2.md#round) function in CTL.
