<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate pattern match -->

##### Validate pattern match

The **Validate pattern match** allows you to validate values in a string column using a pattern defined by a regular expression. You can read more about regular expressions in CloverDX [here](../developer/language-reference-ctl2.md#regular-expressions).

All values that fail the validation are marked as errors in the data set to easily identify them in the data preview. Rows with these errors are automatically rejected and included in the reject file when running the job. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files, and refer to [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, select a string column to validate.
- **Pattern**: required, the regular expression to use in the validation.
- **Accept empty values**: checked by default. When checked, empty values (see [working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty)) are considered valid. When not checked, empty values are reported as validation errors.
- **Error message**: specify the error message that will be associated with the validated value. This message will be displayed when hovering over an invalid value in the dataset or included as the reject reason in the reject file. The default value is *Value does not match regular expression*.

###### Examples

Validation using regular expression patterns is frequently used to validate basic data patterns - for example various identification numbers, date formats and more.

In the following text you can see few basic example patterns that should help you get an idea about how the step works. For more details about how to write complex regular expressions, we recommend looking online for regular expression tutorials. Note that there are many types of regular expression engines that use slightly different syntax. CloverDX uses Java regular expression syntax.

- **Social security numbers**: social security numbers are 9-digit numbers frequently written in three groups - for example 123-45-6789. To validate that a text column matches this format, use regular expression pattern `[0-9]{3}-[0-9]{2}-[0-9]{4}`. Alternatively, you can use `\d{3}-\d{2}-\d{4}`.
- **Tax identification number** in Czech Republic starts with letters CZ and then contains 8 to 10 digits. This can be validated using pattern `CZ[0-9]{8,10}` or `CZ\d{8.10}`. Note that regular expressions are case-sensitive, so this expression will not match value `cz12345678` while it will match `CZ12345678`. If you wish to also accept lower-case form of the number, you can use `(?i)` modifier to enable case-insensitive matching: `(?i)CZ[0-9]{8,10}`.
- **National Insurance Number** in UK is formatted as two prefix letters, six digits and one suffix letter. To validate this in a simple manner, you could use expression like `[A-Z]{2}[0-9]{6}[A-Z]`. However, this will be only very rough validation since not all letters are allowed to be used in prefix or suffix. A more complete pattern would need to exclude certain letters to get `[A-Z&&[^DFIQUV]][A-Z&&[^DFIQUVO]][0-9]{6}[A-D]`.

Note that when using regular expressions, you might be tempted to write regular expressions for credit cards or emails. In those cases we recommend using the [Validate credit card](wrangler-step-validate-credit-card.md) or [Validate email](wrangler-step-validate-email.md) steps instead - they are more powerful and precise and will provide better error message than pure regular expression.

| Input value | Regular expression | Accept empty values | Result |
| --- | --- | --- | --- |
| `"123-45-6789"` | `[0-9]{3}-[0-9]{2}-[0-9]{4}` | Yes | Valid |
| "" (empty value) | `[0-9]{3}-[0-9]{2}-[0-9]{4}` | Yes | Valid |
| "" (empty value) | `[0-9]{3}-[0-9]{2}-[0-9]{4}` | No | Invalid - empty values are not accepted. |
| *null* | (any) | Yes | Valid - empty values are accepted. |
| *null* | (any) | No | Invalid - empty values are not accepted. |
| "XYZ" | X` | Yes | Invalid. Validation applies to the whole value. |
| "XYZ" | `.*X.*` | Yes | Valid. We explicitly allow any characters before and after X. |

###### Remarks

- Validation always applies to whole input value. To match a substring, use wildcards like `.*` before and after your pattern.
- Pattern matching is case-sensitive. To perform case-insensitive matching, add `(?i)` at the beginning of your pattern.

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Regular expressions in CloverDX](../developer/language-reference-ctl2.md#regular-expressions)
- [Validator component in CloverDX Designer](../developer/validator.md)
