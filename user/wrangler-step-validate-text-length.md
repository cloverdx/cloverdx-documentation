<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate text length -->

##### Validate text length

The **Validate text length** step allows you to validate if values in a string column match the specified length range (i.e., number of characters). Strings that are too long or too short are marked as invalid and will be shown in the data preview and written to a reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files and [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, select a string column to validate.
- **Minimum length**: optional[[1]](wrangler-step-validate-text-length.md#wrangler-step-validate-text-length-fn1), specify the minimum[[2]](wrangler-step-validate-text-length.md#wrangler-step-validate-text-length-fn2) value length. When not specified, all strings with at most **Maximum length** characters are considered valid.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Maximum length**: optional[[1]](wrangler-step-validate-text-length.md#wrangler-step-validate-text-length-fn1), specify the maximum[[2]](wrangler-step-validate-text-length.md#wrangler-step-validate-text-length-fn2) value length. When not specified, all strings with at least **Minimum length** characters are considered valid.
  - **Constant value**: enter a constant value.
  - **Select from column**: choose a column with integer values. The value from each row will be applied to the corresponding row in the input column.
- **Accept empty values**: configure whether empty values are considered empty or not. By default, this option is checked (i.e., empty values are valid).
- **Error message**: configure custom error message that is associated with invalid values and is be displayed when hovering over an invalid value in the data preview. Default error message is *Value length is outside of allowed range*.

Note that all characters, including trailing and leading white spaces, are counted when calculating the total number of characters in a string.

| 1 | At least one of the boundaries must be specified. |
| --- | --- |
| 2 | The **Maximum value** must be greater than the **Minimum value**. |

###### Examples

| Input value | Minimum length | Maximum length | Accept empty Values | Input value length | Result | Description |
| --- | --- | --- | --- | --- | --- | --- |
| `INV7854784` | 8 | 10 | Any | 10 | Valid | Value is within the 8-10 range. |
| `INV00045565` | 8 | 10 | Any | 11 | Invalid | Value is not within the 8-10 range. |
| `INV4589` | 8 | 10 | Any | 7 | Invalid | Value is not within the 8-10 range. |
| `" INV4589 "` | 8 | 10 | Any | 11 | Invalid | Value is not within the 8-10 range because 2 leading and 2 trailing space characters are present. |
| `T` | 1 | 1 | Any | 1 | Valid | Value has exactly 1 character. |
| `True` | 1 | 1 | Any | 4 | Invalid | Value has more than 1 character. |
| `INV35` | - | 10 | Any | 5 | Valid | Value has less than 10 characters. |
| `INV0056544589` | 8 | - | Any | 13 | Valid | Value has more than 8 characters. |
| *No value* | Any | Any | Yes (checked) | 0 | Valid | Valid because the *Accept empty values* option is checked. |
| *No value* | Any | Any | Yes (checked) | 0 | Invalid | Invalid because the *Accept empty values* option is unchecked. |

###### Remarks

- If you want to ensure that there are no trailing or leading spaces prior to the validation, use the [Trim step](wrangler-step-trim.md) first.

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
