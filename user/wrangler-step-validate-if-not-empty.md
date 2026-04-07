<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate if not empty -->

##### Validate if not empty

The **Validate if not empty** step allows you to identify all empty values (see [working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty)) in the specified columns and mark them as validation errors. All invalid rows are automatically rejected at the end of the job and written to the reject file. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files and [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Columns to validate**: required, select one or more columns to test whether they are empty or not. If multiple columns are selected, all of them must have non-empty values for the row to be considered valid.
- **Error message**: specify the error message that will be associated with the validated values of the columns that are empty. If multiple columns have empty values, all of them will be marked as invalid. This error message will be displayed when hovering over an identified empty value in the data set and included as the reject reason in the reject file. It defaults to "Value cannot be empty".

###### Examples

The step was configured to identify empty values in a column containing email addresses.

| Input value | Result | Description |
| --- | --- | --- |
| `john.smith@testcompany.com` | Valid | The value is not empty. |
| *No value* | Invalid | An empty value is identified. |
| `" "` (all spaces) | Valid | Space characters are not considered empty values. Use [`isBlank`](../developer/string-functions-ctl2.md#isblank) function and [Validate with formula step](wrangler-step-validate-with-formula.md) to validate value like this. |

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
