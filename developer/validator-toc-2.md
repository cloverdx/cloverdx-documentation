<!-- Development > Component reference > Data Quality > Validator > List of rules -->

#### List of rules

- [Basic rules](validator-toc-2.md#basic-rules)
  - [Empty/Nonempty field](validator-toc-2.md#emptynonempty-field)
  - [Empty/Nonempty subset](validator-toc-2.md#emptynonempty-subset)
  - [Comparison](validator-toc-2.md#comparison)
  - [Interval](validator-toc-2.md#interval)
  - [Expression](validator-toc-2.md#expression)
  - [Lookup](validator-toc-2.md#lookup)
  - [Accept](validator-toc-2.md#accept)
  - [Reject](validator-toc-2.md#reject)
- [String rules](validator-toc-2.md#string-rules)
  - [Is Date](validator-toc-2.md#is-date)
  - [Is Number](validator-toc-2.md#is-number)
  - [String Length](validator-toc-2.md#string-length)
  - [Pattern Match](validator-toc-2.md#pattern-match)
  - [Enum Match](validator-toc-2.md#enum-match)
  - [Email Address](validator-toc-2.md#email-address)
  - [Phone Number](validator-toc-2.md#phone-number)
- [Assignment rules](validator-toc-2.md#assignment-rules)
  - [Copy](validator-toc-2.md#copy)
  - [Transform](validator-toc-2.md#transform)
  - [Copy all fields by name](validator-toc-2.md#copy-all-fields-by-name)
- [Custom rules](validator-toc-2.md#custom-rules)
- [Imports](validator-toc-2.md#imports)

##### Basic rules

There are following validation rules: [Empty/Nonempty field](validator-toc-2.md#emptynonempty-field), [Empty/Nonempty subset](validator-toc-2.md#emptynonempty-subset), [Comparison](validator-toc-2.md#comparison), [Interval](validator-toc-2.md#interval), [Expression](validator-toc-2.md#expression), [Lookup](validator-toc-2.md#lookup), [Accept](validator-toc-2.md#accept) and [Reject](validator-toc-2.md#reject).

###### Empty/Nonempty field

Rule checks whether the field is empty or nonempty according to the rule settings.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | startDate |
| Output field | Field to that data will be written. | startDate |
| Valid | Which content - empty or nonempty - should be considered as valid. | Nonempty field |
| Custom reject message | Error message defined by the user, mapped to field **validationMessage**. | The field is not a natural number. |
> [!NOTE]
> Rule usage example
> Field address has to contain any nonempty value.

###### Empty/Nonempty subset

Rule checks whether at least `n` of `m` selected fields are empty or nonempty according to the rule settings.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input fields | Fields to be validated | startDate, endDate, tariff |
| Count | Should be counted empty or nonempty fields. | Nonempty fields |
| Minimal count | Number of empty (or nonempty) field needed to pass validation. | 2 |
| Custom reject message | Error message defined by user, mapped to field **validationMessage**. | Not enough contact details. |
> [!NOTE]
> Rule usage example
> At least 2 of the fields phone, email, and address must have a nonempty value.

###### Comparison

This rule compares the incoming field value with constant set up in rule parameters.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | age |
| Output field | Field to that data will be written. | age |
| Compare as | Data type used for comparison. For example 5 is lower than 10 if any numeric type is set up here, but 5 is greater than 10 using string (alphabetical) comparison. | Decimals |
| Operator | An operator used for comparison between a constant on the following line and a field value. | >= |
| Compare with | A field is being compared against this value. | 21 |
| Accept empty values | If checked, empty string and null are considered as valid values. | false |
| Custom reject message | An error message defined by the user, mapped to the field**validationMessage**. | Too young. |
> [!NOTE]
> Rule usage example.
> Rule usage example: Age in years has to be greater or equal to 21.

###### Interval

This rule checks whether the incoming field value is in the specified interval.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | A field to be validated | weight |
| Output field | A field to that data will be written. | weight |
| Compare as | A data type used for comparison. | decimals |
| Boundaries | Set whether include or not limit values. | From exclusive, to inclusive |
| From | Lower limit | 480 |
| To | Upper limit | 520 |
| Accept empty values | If checked, empty string and null are considered as valid values. | true |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Not enough heavy or too heavy. |
> [!NOTE]
> Rule usage example
> Rule usage example: Weight in kilograms has to be greater than 480 and lower or equal than 520.

###### Expression

Evaluates a CTL expression and rejects validated record when the result is false.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Expression | CTL expression to be evaluated for each validated record | $in.0.startTime < $in.0.endTime |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Start time greater than end time. |
> [!NOTE]
> Rule usage example
> Start time is lower than end time. Records where start time is greater than end time will be rejected.
> [!NOTE]
> Filter expression editor helps editing the CTL expression.

###### Lookup

Checks if a value is present or missing in a lookup table.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Lookup name | Name of the lookup table. The table needs to be present in the current graph. | MyLookupTable |
| Key mapping | Mapping between fields from lookup table to data fields. | tableField:=dataField |
| Action on match | Which records should be interpreted as valid: A record with fields having a value in the lookup table or records having values not present in the lookup table. | Reject record |
| Custom reject message | Error message defined by user, mapped to field **validationMessage**. | Unknown product. |
> [!NOTE]
> Rule usage example
> Product code is a valid product code from the table. Consider all record not having corresponding product code in the lookup table as invalid.
> [!NOTE]
> The data field and corresponding field from the lookup table need to have same data type.

###### Accept

The rule accepts any field.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

###### Reject

The rule rejects any record.

The rule can be found in [Basic rules](validator-toc-2.md#basic-rules).

##### String rules

**String rules** contains following **available validation rules:**[Is Date](validator-toc-2.md#is-date), [Is Number](validator-toc-2.md#is-number), [String Length](validator-toc-2.md#string-length), [Pattern Match](validator-toc-2.md#pattern-match), [Enum Match](validator-toc-2.md#enum-match), [Email Address](validator-toc-2.md#email-address) and [Phone Number](validator-toc-2.md#phone-number).

###### Is Date

Rule **Is Date** checks string field to be in desired date and time format. See [Date and time format](metadata-records-and-fields.md#date-and-time-format)

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | startDate |
| Output field | Having successfully converted the value from string to date the converted value is being assigned to the field with this name in output record on port 0. | start_date |
| Accept empty values | If checked, empty string and null are considered as valid values. | false |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Invalid start date. |
> [!NOTE]
> Rule usage example
> Check start date to be in format yyyy-MM-dd.
> [!NOTE]
> Functionality of date validation depends on correct locale and timezone settings. See [Locale](metadata-records-and-fields.md#locale) and [Time zone](metadata-records-and-fields.md#timezone).
> [!IMPORTANT]
> If you have date in the `yyyyMMdd` format (e.g. 20150111) and you need to have exactly 8 characters, use **Strict validation** from [Locale and format settings](validator.md#locale-and-format-settings) to check date correctly. Otherwise `2011011` would be considered as valid date corresponding to the mask. The date would be interpreted as `2011-01-01`.

###### Is Number

Rule **Is Number** validates field to have a desired [numeric format](metadata-records-and-fields.md#numeric-format).

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | weight |
| Output field | Having successfully converted the field value to number of predefined type, the numeric value is assigned to the output field of name specified here. | weight_as_number |
| Number data type | Numeric data type | integer |
| Accept empty values | If checked, empty string and null are considered as valid values. | true |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Non-numeric value found in field weight. |
> [!NOTE]
> Rule usage example
> Weight must be an integer.

###### String Length

Rule **String Length** checks the length of the string.

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | userName |
| Output field | Field to that data will be written. | userName |
| Minimal length | Lower bound of length comparison. | 3 |
| Maximal length | Upper bound of length comparison. | 20 |
| Accept empty values | If checked, empty string and null are considered as valid values. | false |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | User name too short or too long. |
> [!NOTE]
> Rule usage example
> Login name must have at least 3 characters. The maximal allowed length is 20 characters.

###### Pattern Match

The **Pattern Match** rule checks whether the field corresponds to a regular expression.

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | name |
| Output field | Field to that data will be written. | name |
| Pattern to match | Regular pattern used for comparison. | A[a-z]{2}.* |
| See [Regular expressions](language-reference-ctl2.md#regular-expressions) |  |  |
| Ignore case | Ignores differences between lower case and upper case letters. If the field is checked, lower case and upper case letters will be considered as same. | False |
| Accept empty values | If checked, empty string and null are considered as valid values. | false |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Name does not begin with A or does not have at least three letters. |
> [!NOTE]
> Rule usage example
> Check the name to begin with letter A and to be formed by at least 3 letters.
> [!NOTE]
> If your regular expression does not match the string and you expect that it should match, you probably need *pattern flag*, e.g. `(?s).*`. See [Regular expressions](language-reference-ctl2.md#regular-expressions)

###### Enum Match

The **Enum Match** rule checks a field to contain one of values from a predefined set of values.

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | reportedCount |
| Output field | Field to that data will be written. | reported count |
| Compare as | Data type used for comparison. For example 5 is lower than 10 if any numeric type is set up here, but 5 is greater than 10 using string (alphabetical) comparison. | Decimals |
| Accept values | Set of values considered as valid. | A,B |
| Ignore case | Ignores differences between lower case and upper case values. | True |
| Accept empty values | If checked, empty string and null are considered as valid values. | false |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Value not out of the set. |
> [!NOTE]
> Rule usage example
> Field must have value of "A" or "B".

###### Email Address

The **Email Address** rule checks a field to be valid email address. Valid email address means an email address in correct format. It does not mean existing email address.

The rule can be found in [String rules](validator-toc-2.md#string-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | senderEmail |
| Output field | Field to that data will be written. | senderEmail |
| Plain e-mail address only | Allows email addresses in the form like "[john@sea.com](mailto:john@sea.com)" only. If the checkbox is checked, addresses like "<[john@sea.com](mailto:john@sea.com)>" will be considered as invalid. | True |
| Allow group addresses | Allows deprecated group address format (see [RFC 822](http://www.ietf.org/rfc/rfc0822.txt)) to be considered as valid email address too. Group format is in the form: "Group: john@sea, francis@ocean". Opening string with a colon is necessary. | True |
| Allow addresses with no TLD | Allows addresses with no top-level domain, like "admin@mailserver1". | False |
| Accept empty values | If checked, empty string and null are considered as valid values. | true |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Sender email is invalid |
> [!NOTE]
> Rule usage example
> Check that field senderEmail contains valid email address.

###### Phone Number

The **Phone Number** rule checks a field for a phone number in correct format.

The rule can be found in [String rules](validator-toc-2.md#string-rules).

Furthermore the rule can convert a validated phone number to a specified format.

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be validated | customerPhoneNumber |
| Output field | Field to that data will be written. | validatedPhoneNumber |
| Region | Phone numbers of which region are considered as valid. When this field is not specified, only international phone numbers (start with + sign) are accepted. | US - United Stated (+1)1) |
| Phone number pattern | An optional parameter. Phone number being validated must match the specified pattern. When not specified, an arbitrary format is accepted, but still only certain formatting characters are allowed. | +1 DDD.DDD.D{3,5}2) |
| Accept empty values | Empty values are considered as a valid phone number. | true |
| Output format | The rule enables to get a phone number in several formats. 3) | E.164 ITU-T Recommendation (+41446681800) |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Invalid phone number |

1) (201) 555-5555 is a valid US number, but so is +420 777 777 777 - it is a valid international phone number that you can dial from the US.

2) Usage: D substitutes any digit. You can also specify allowed repetition count with {min,max} pattern.

3) The following output formats of phone numbers are available:

- Original input value
- E.164 ITU-T Recommendation (+41446681800)
- International format - E.123 ITU-T Recommendation (+41 44 668 1800)
- National format - E.123 ITU-T Recommendation (044 688 1800)
- tel: URI RFC 3966 (tel: +41-44-668-1800)
> [!NOTE]
> Rule usage example
> Phone number has to be valid US number with leading international prefix.

##### Assignment rules

**Assignment rules** serve data manipulation within Validator.

These rules do not affect the result of the validation - that is, their result is neither valid nor invalid. Their validation result will neither make an **AND** group fail nor an **OR** group succeed.

There are following assignment rules available: [Copy](validator-toc-2.md#copy), [Transform](validator-toc-2.md#transform) and [Copy all fields by name](validator-toc-2.md#copy-all-fields-by-name).

###### Copy

**Copy** copies a value of an input field to another output field.

The rule can be found in [Assignment rules](validator-toc-2.md#assignment-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Input field | Field to be copied | startDate |
| OutputField | An output field for a value copied from the field above. | startDateStr |
> [!NOTE]
> Rule usage example
> Copy a content of the field **startDate** to the field **startDateStr**.

###### Transform

**Transform** can be used to produce custom output values.

The rule can be found in [Assignment rules](validator-toc-2.md#assignment-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Transform | A transformation in CTL. For detailed information about **CloverDX** Transformation Language, see [CTL2 - CloverDX Transformation Language](part5.md). Return values `SKIP` and `STOP` apply. `SKIP` causes no output to be produced, `STOP` aborts the validation. See [Return values of transformations](transformations.md#return-values-of-transformations). |  |
> [!NOTE]
> Rule usage example
> Copy a group of input fields to a different group of output fields based on which branch of validation tree (group of rules) was successful.

###### Copy all fields by name

**Copy all fields by name** copies all input fields onto output fields having the same name and type.

The rule is added as a first rule in a tree of active validation rules, by default. The rule should not be put after any rule assigning values to output fields as it would overwrite all the output values produced by rules above it.

The rule can be found in [Assignment rules](validator-toc-2.md#assignment-rules).

##### Custom rules

**Custom rules** are validation rules written in CTL2. CTL2 code of user defined validation rule contains a function returning a **boolean** with the same name as is the rule name. The rule can have one or more rule parameters.

**Custom rules** can be found in [Available rules](validator.md#available-rules).

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Parameter mapping | Mapping of fields to function parameters. | param1:=product |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | Invalid product code. |
> [!IMPORTANT]
> Due to rule name - function name binding the Validator can **not** work with **overloaded** CTL2 functions (functions with the same name but different set of input parameters).

##### Imports

**Imports** enables to link an external file with CTL functions and use the functions as Validation rules. The imported file or files can contain any type of CTL functions but only functions returning **boolean** are listed in available validation rules and can be used as validation rules.

Editing of linked files containing CTL functions is accessible from the dialog: Select the desired file and click on the **edit** icon below the list of **available rules**.

| Parameter name | Parameter description | Value example |
| --- | --- | --- |
| Parameter mapping | Mapping of fields to function parameters. | param2:=postCode |
| Custom reject message | An error message defined by the user, mapped to the field **validationMessage**. | The postcode is not valid. |
