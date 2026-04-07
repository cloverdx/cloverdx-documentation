<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate phone number -->

##### Validate phone number

The **Validate phone number** step allows you to validate phone numbers. The step understands the phone number formats and regional differences between phone numbers (like the number of digits, prefixes, …​) and will verify that the number follows the rules for the selected region.

This step does not try to validate whether the number exists - it validates the format of the number only.

All values that fail the validation are marked as errors in the dataset to easily identify them in the data preview, and rows with these errors are automatically rejected and included in the reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files, and refer to [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, a string or integer column containing phone numbers with one number per row.
- **Region**: select which region to use when validating the numbers. The region defines rules that the phone numbers must follow - for example, the number of digits, prefixes, area codes, and more. Typically, regions represent countries - like the Unites States, Germany, and many others. One special region - *None* - is provided in case you do not have any specific regional requirements for the numbers. This region requires phone numbers to have international dialing the prefix (e.g., +1 etc.).
- **Accept empty**: configure whether an empty value is considered a valid phone number. An empty value is a value that is either `null` (shown as *No value* in data preview), a zero-length string, or a string composed entirely of whitespaces. By default, this is checked (i.e., empty values are considered valid).

###### Examples

| Input value | Accept empty values | Region | Result | Description |
| --- | --- | --- | --- | --- |
| `478.629.2062` | Any | US | Valid | Valid US phone number. |
| `478 629.2062` | Any | US | Valid | Valid US phone number - whitespaces before and in the middle do not affect the validity of the number. |
| `+44 (0) 203 789 2070` | Any | US | Valid | Numbers with international dialing code (+44 - UK in this example) are valid even if a specific region is selected (e.g., US). These numbers can be dialed from any country and if they match the local rules as defined by their dialing code, they are considered valid. |
| *No value* | Yes (checked) | Any | Valid | This is a valid number since *Accept empty* is checked. |
| *No value* | No (unchecked) | Any | Invalid | Invalid since empty values are not allowed as per the *Accept empty* setting. |

###### Remarks

- Only the syntax of the phone number is checked. The step does not try to verify that the phone number exists or is assigned to a user.
- Running validation on an *Error* value does not try to validate the value and instead produces an *Error* right away.

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
