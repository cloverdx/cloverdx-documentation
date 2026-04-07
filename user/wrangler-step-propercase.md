<!-- End user’s guide > Wrangler user guide > Transformation steps > Text manipulation steps > Propercase -->

##### Propercase

**Propercase** step capitalizes first letters of each word and lowercases all other letters. The step can only be applied to string columns.

###### Parameters

- **Input column**: required, a string column containing input text.
- **Target column**: required, configure the column which will receive the output. The output will always be of string type.
  - **Write result to the current column**: overwrite the **Input column** with the result.
  - **Create new column with name**: create a new column with specified name. Name of the new column can contain spaces or special characters - technical column name will be created automatically. The new column will be placed right after the **Input column**.

###### Examples

| Input value | Output value | Explanation |
| --- | --- | --- |
| "product code name" | "Product Code Name" | First letters of all words are capitalized. |
| "PRODUCT CODE NAME" | "Product Code Name" | First letters of all words remain capitalized, other letters are converted to lowercase. |
| "ProDuct cOde name" | "Product Code Name" | First letters of all words are capitalized, and the uppercase letters in the middle of the words are converted to lowercase. |

###### See also

- [Lowercase step](wrangler-step-lowercase.md)
- [Uppercase step](wrangler-step-uppercase.md)
- [`properCase`](../developer/string-functions-ctl2.md#propercase) function in CTL.
