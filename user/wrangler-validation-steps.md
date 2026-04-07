<!-- End user’s guide > Wrangler user guide > Transformation steps > Data validation (data quality) steps -->

#### Data validation (data quality) steps

Validation steps allow you to verify that your data is in the desired format. All values that fail the validation are highlighted in the dataset and marked as errors in the data preview to easily locate them. The number of errors is also included in the [data quality bar](transforming-data.md#data-quality-bar).

When you run a job that includes data errors, all rows with invalid values are automatically excluded from the output and placed in a reject file. See [Job Run Details](transforming-data.md#job-run-details) for more information on the reject files.

For our recommendations on how to deal with data errors, see [fixing errors](transforming-data.md#fixing-errors).

**List of validation steps:**

- [Validate against list](wrangler-step-validate-against-list.md): validate if a value is in a list of allowed values.
- [Validate credit card](wrangler-step-validate-credit-card.md): validate format of credit card numbers.
- [Validate email](wrangler-step-validate-email.md): validate format of email addresses.
- [Validate if not empty](wrangler-step-validate-if-not-empty.md): validate if values are not empty.
- [Validate pattern match](wrangler-step-validate-pattern-match.md): validate if values match a pattern.
- [Validate phone number](wrangler-step-validate-phone-number.md): validate format of phone numbers with support for international number formats.
- [Validate text length](wrangler-step-validate-text-length.md): validate text length.
- [Validate value range](wrangler-step-validate-value-range.md): validate if values are within specified range.
- [Validate with formula](wrangler-step-validate-with-formula.md): validate data using your custom formula.
