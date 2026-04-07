<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate value range -->

##### Validate value range

The **Validate value range** step allows you to validate if values in a column match the specified value range. All values that fail the validation are marked as validation errors in the data set and rows with these errors are automatically rejected and included in the reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files and [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, select a column to validate. You can select any column with types that can be sorted - string, decimal, integer as well as date columns.
- **Minimum value**: optional[[1]](wrangler-step-validate-value-range.md#wrangler-step-validate-value-range-fn1), enter the minimum[[2]](wrangler-step-validate-value-range.md#wrangler-step-validate-value-range-fn2) value. If not specified, the minimum is not tested (i.e., there is no lower bound for the value).
- **Maximum value**: optional[[1]](wrangler-step-validate-value-range.md#wrangler-step-validate-value-range-fn1), enter the maximum[[2]](wrangler-step-validate-value-range.md#wrangler-step-validate-value-range-fn2) value. If not specified, the maximum is not tested (i.e., there is no upper bound for the value).
- **Include minimum**: configure whether the minimum is included in the range or not (i.e., whether the range is closed or open on the lower bound). When checked, the minimum value is included in the range - values larger than or equal to the minimum are valid. When unchecked, only values larger than the minimum are valid. By default, this is checked.
- **Include maximum**: configure whether the maximum is included in the range or not (i.e., whether the range is closed or open on the upper bound). When checked, the maximum value is included in the range - values smaller than or equal to the maximum are valid. When unchecked, only values smaller than the maximum are valid. By default, this is checked.
- **Ignore case for string values**: configure whether string comparisons are case-sensitive or not. If checked, the value comparison is not case-sensitive. By default, this option is checked.
- **Accept empty values**: configure whether empty values (see [working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) for more information) are considered valid or not. If checked, empty values are considered valid. This option is checked by default.
- **Error message**: configure a custom error message that will be associated with invalid values. The error message is displayed when hovering over an invalid value in the data preview and is included as the reject reason in the reject file. The default error message is *Value is out of allowed range*.
Entering value range
When configuring **Minimum value** and **Maximum value** for the step, the following rules apply depending on the data type:

- **Integer columns**: do not use any digit grouping symbol (i.e., write *1234* instead of *1,234*).
- **Decimal columns**: you must use period as the decimal separator and you must not use any digit grouping symbols (i.e., write *1234.56* and not *1,234.56*).
- **Date columns**: dates must be entered in one of the following formats:
  - `yyyy-MM-dd HH:mm:ss` (e.g., `2023-08-01 08:09:07`)
  - `yyyy-MM-dd HH:mm` (e.g., `2023-08-01 08:09`)
  - `yyyy-M-d H:m:s` (e.g., `2023-8-1 8:9:7`)
  - `yyyy-M-d H:m` (e.g., `2023-8-1 8:9`)
  - `yyyy-M-d` (e.g., `2023-8-1`) - in this case, the date is considered as `2023-08-01 0:00:00`

| 1 | At least one of the boundaries must be specified. |
| --- | --- |

| 2 | The **Maximum value** must be greater than the **Minimum value**. |
| --- | --- |

###### Examples
String columns
The following examples show how the step can be used when validating string columns.

| Input value | Min value | Max value | Include minimum | Include maximum | Ignore case | Accept empty values | Result | Description |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `INV33333` | INV30000 | INV40000 | Yes (checked) | Yes (checked) | Yes (checked) | Any | Valid | Value is within the specified range. |
| `inv33333` | INV30000 | INV40000 | Yes (checked) | Yes (checked) | No (unchecked) | Any | Invalid | Value is not valid because the *Ignore case for string values* option is unchecked. |
| `INV30000` | INV30000 | INV40000 | Yes (checked) | Yes (checked) | Yes (checked) | Any | Valid | Value is within the specified range because the *Include minimum* option is checked. |
| `INV30000` | INV30000 | INV40000 | No (unchecked) | Yes (checked) | Yes (checked) | Yes (checked) | Invalid | Value is not within the specified range because the *Include minimum* option is unchecked. |
| `INV40000` | INV30000 | INV40000 | Yes (checked) | Yes (checked) | Yes (checked) | Any | Valid | Value is within the specified range because the *Include maximum* option is checked. |
| `INV40000` | INV30000 | INV40000 | Yes (checked) | No (unchecked) | Yes (checked) | Any | Invalid | Value is not within the specified range because the *Include maximum* option is unchecked. |
Decimal and integer columns
The following table provides examples of the step usage for numeric columns - decimals or integers.

| Input value | Min value | Max value | Include minimum | Include maximum | Ignore case | Accept empty values | Result | Description |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `9.99` | 8.50 | 14.50 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range. |
| `8.50` | 8.50 | 14.50 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range because the *Include minimum* option is checked. |
| `8.50` | 8.50 | 14.50 | No (unchecked) | Yes (checked) | Any | Any | Invalid | Value is not within the specified range because the *Include minimum* option is unchecked. |
| `14` | 8 | 14 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range because the *Include maximum* option is checked. |
| `14` | 8 | 14 | Yes (checked) | No (unchecked) | Any | Any | Invalid | Value is not within the specified range because the *Include maximum* option is unchecked. |
Date columns
The following table provides examples of how to use the step to validate date columns.

| Input value | Min value | Max value | Include minimum | Include maximum | Ignore case | Accept empty values | Result | Description |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `2023-03-03` | 2023-01-01 00:00:00 | 2023-07-01 00:00:00 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range. |
| `2023-01-01` | 2023-01-01 00:00:00 | 2023-07-01 00:00:00 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range because the *Include minimum* option is checked. |
| `2023-01-01` | 2023-01-01 00:00:00 | 2023-07-01 00:00:00 | No (unchecked) | Yes (checked) | Any | Any | Invalid | Value is not within the specified range because the *Include minimum* option is unchecked. |
| `2023-07-01` | 2023-01-01 00:00:00 | 2023-07-01 00:00:00 | Yes (checked) | Yes (checked) | Any | Any | Valid | Value is within the specified range because the *Include maximum* option is checked. |
| `2023-07-01` | 2023-01-01 00:00:00 | 2023-07-01 00:00:00 | Yes (checked) | No (unchecked) | Any | Any | Invalid | Value is not within the specified range because the *Include maximum* option is unchecked. |
Empty values
| Input value | Min value | Max value | Include minimum | Include maximum | Ignore case | Accept empty values | Result | Description |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| *No value* | Any | Any | Any | Any | Any | Yes (checked) | Valid | Valid because the *Accept empty values* option is checked. |
| *No value* | Any | Any | Any | Any | Any | No (unchecked) | Invalid | Invalid because the *Accept empty values* option is unchecked. |

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
