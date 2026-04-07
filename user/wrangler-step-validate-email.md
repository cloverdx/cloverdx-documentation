<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate email -->

##### Validate email

The **Validate email** step allows you to validate syntax of an email address. The step only verifies the syntax of the email address - for example, that it has proper local and domain names, that it contains the "@" symbol etc. This step does not try to send an email to verify the existence of the email address.

All values that fail the validation are marked as errors in the dataset to easily identify them in the data preview, and rows with these errors are automatically rejected and included in the reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files, and refer to [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, a string column containing email addresses with one address per row.
- **Accept empty values**: configure whether an empty value is considered a valid email. Empty value is a value that is either `null` (shown as *No value* in data preview), zero-length string or a string composed entirely of whitespaces. By default, this is checked (i.e., empty emails are considered valid).

###### Examples

| Input value | Accept empty values | Result | Description |
| --- | --- | --- | --- |
| `example@example.com` | Any | Valid | A valid email. |
| `example@example.com` | Any | Valid | The step strips out leading and trailing whitespaces before validation so this is a valid email. |
| `example @ example.com` | Any | Invalid | Email address cannot contain whitespaces in the middle - these are not removed during the validation. |
| `example.example.com` | Any | Invalid | An invalid email missing the domain part. |
| *No value* | Yes (checked) | Valid | This is valid email since *Accept empty values* is checked. |
| *No value* | No (unchecked) | Invalid | Invalid since empty values are not allowed as per *Accept empty values* setting. |

###### Remarks

- The step only validates syntax of the email. It does not verify that the email (or even its domain) exists.
- Running validation on an *Error* value does not try to validate the value and instead produces an *Error* right away.

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
