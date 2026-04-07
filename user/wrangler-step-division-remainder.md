<!-- End user’s guide > Wrangler user guide > Transformation steps > Math steps > Division remainder -->

##### Division remainder

The **Division remainder** step computes a remainder after division of the first argument with the second argument (same as % operator).

###### Parameters

- **Input column**: required, an integer column containing the data divide by the **Divisor**.
- **Divisor**: required, an integer value used as a divisor. The value cannot be zero as that will cause "division by zero" error.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Target column**: required, configure the column which will receive the output. Output will always be of integer type.
  - **Write result to the current column**: overwrite the input column with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the input column.

###### Examples

| Input value | Divisor | Output value | Description |
| --- | --- | --- | --- |
| 10 | 3 | 1 | 10 % 3 = 1  (10 / 3 has remainder 1) |
| 10 | 5 | 0 | 10 % 5 = 0  (10 / 5 has remainder 0) |
| -10 | 5 | 0 | -10 % 5 = 0  (-10 / 5 has remainder 0) |
| *No value* | 5 | *No value* | Empty or missing value will not return *Error*. |
| *any value* | 0 | *Error* | Division by zero is not allowed. |

###### Remarks

- **Divisor** input parameter allows only positive whole numbers.

###### See also

- [Calculate formula step](wrangler-step-formula.md)
