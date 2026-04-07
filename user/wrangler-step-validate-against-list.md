<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps > Validate against list -->

##### Validate against list

The **Validate against list** step allows you to validate values in a string column against a list of specified values (i.e., against enumeration). All values that are not found in the list are marked as invalid. Invalid values will be visible in the data preview and in the reject file. See [Job Run Details](transforming-data.md#job-run-details) for more information on reject files and [fixing errors](transforming-data.md#fixing-errors) for our recommendations on how to deal with data errors.

###### Parameters

- **Input column**: required, select a string column to validate.
- **Values**: required, enter the values to validate against. Values are entered as plain text with each value specified on a separate line. Lines are trimmed (their leading and trailing spaces are removed) before they are considered. Ordering of values does not matter.
- **Ignore case**: checked by default. When checked, the validation is not case-sensitive (i.e., lower-case and upper-case letter are considered to be the same). If unchecked, value comparison is case sensitive, so "red" is not the same as "RED".
- **Accept empty values**: checked by default. When checked, empty values (see [working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty)) are considered valid. If not checked, empty values are considered invalid, and the row will be rejected.
- **Error message**: required, configure an error message that will be associated with invalid values. The error message is displayed when hovering over an identified empty value in the data set and included as the reject reason in the reject file. Default error message is *Value is not in the allowed values list*.

###### Examples

In the following examples we will test whether currency code is **EUR** or **USD**.

| Input value | Ignore case | Accept empty values | Result | Description |
| --- | --- | --- | --- | --- |
| `EUR` | Yes (checked) | Any | Valid | Value is in the list of valid values. |
| `eur` | Yes (checked) | Any | Valid | Value is in the list of valid values and the case is ignored. |
| `eur` | No (unchecked) | Any | Invalid | Value is in the list of valid values but the *Ignore case* option is unchecked. |
| `CZK` | Yes (checked) | Any | Invalid | Value is not in the list of valid values. |
| *No value* | Any | Yes (checked) | Valid | Valid because the *Accept empty values* option is checked. |
| *No value* | Any | No (unchecked) | Invalid | Invalid because the *Accept empty values* option is unchecked. |
| "    " (4 spaces) | Any | Yes (checked) | Invalid | String consisting of all white spaces is not considered empty and also does not appear in the list of allowed values. |

###### Remarks

- If you have multi-line values or values with tab characters to validate, you can use escape sequences (`\n`, `\t`, etc.). For example enter `Baker Street 221b\nNW1 6XE\nLondon` to validate the following multi-line value:

```
Baker Street 221b
NW1 6XE
London
```

- To use a backslash itself as a delimiter, enter two backslashes.

###### See also

- [Validation steps](wrangler-validation-steps.md)
- [Validator component in CloverDX Designer](../developer/validator.md)
