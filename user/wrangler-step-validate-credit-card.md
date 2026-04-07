<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate credit card -->

##### Validate credit card

The **Validate credit card** step allows you to validate credit card numbers. The step validates the format of the number using the Luhn algorithm. The step can, therefore, detect card numbers with typos or missing digits, but it does not try to contact any credit card provider to verify that the credit card exists.

All values that fail the validation are marked as errors in the dataset to easily identify them in the data preview, and rows with these errors are automatically rejected and included in the reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files, and refer to [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, a string or integer column containing credit card numbers with one card per row.
- **Accept empty values**: configure whether an empty value is considered a valid credit card. Empty value is a value that is either `null` (shown as *No value* in data preview), zero-length string or a string composed entirely of whitespaces. By default, this is checked (i.e., empty values are considered valid).

###### Examples

| Input value | Accept empty values | Result | Description |
| --- | --- | --- | --- |
| `3579099126677753` | Any | Valid | Credit card written without any delimiters is accepted. |
| `3579099126677754` | Any | Invalid | In this case the checksum digit is not valid (last digit in the number). |
| `3576-9755-3407-6980` | Any | Valid | Cards with *en dashes* (-) are accepted. |
| `3576—9755—3407—6980` | Any | Invalid | Cards with *em dashes* (—) are considered invalid. |
| `3576 9755 3407 6980` | Any | Valid | Cards with spaces are accepted. |
| `3576-- 9-- 755-3407-6980` | Any | Valid | Position and number of *en dashes* (-) and/or spaces do not impact the validity of the card number. |
| `3576*9755*3407*6980` | Any | Invalid | Star symbol is not allowed as a delimiter and this number is, therefore, considered invalid. |
| *No value* | Yes (checked) | Valid | This is a valid number since *Accept empty values* is checked. |
| *No value* | No (unchecked) | Invalid | Invalid since empty values are not allowed as per *Accept empty* setting. |
| *Error* | Any | *Error* | Calling the step on an *Error* will not run any validation and return an *Error*. |

###### Remarks

- Only the syntax of the credit card number is verified. When checking the syntax, spaces and *en dashes* (-) are ignored. Any other delimiter characters will cause the card number to be considered invalid.
- The step does not attempt to contact any credit card or payment provider to verify the existence of the credit card number.
- Running validation on an *Error* value does not try to validate the value and instead produces an *Error* right away.

###### See also

- [Validation steps](wrangler-validation-steps.md)
