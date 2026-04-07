<!-- End user’s guide > Wrangler user guide > Transformation steps > Data set manipulation steps > Split column -->

##### Split column

The **Split column** step can be used to split data from one string column into multiple columns based on a delimiter.

###### Parameters

- **Input column**: required, select a string column to split.
- **Delimiter**: required, specify a delimiter to be used to split the data.
  - Both single characters (including a space) and multiple characters can be used as delimiters.
  - You can also select newline or tab characters as delimiters from the dropdown list.
- **Number of columns**: required, enter the number of columns the data should be split into.
  - The newly created columns keep the **Input column** name and include *part 1*, *part 2*, etc., in the column names.
  - If the result is an empty value, *No value* is displayed. See [Working with empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) for more information.
  - If the number of columns to be created is lower than the number of the resulting split values, the last column will include the remaining values in the unsplit form.

###### Examples

**Example1:** The *Phone number* column sometimes includes multiple phone numbers, separated by commas.

- Result of spliting into 2 columns:

| Phone number | Phone number part 1 | Phone number part 2 |
| --- | --- | --- |
| +17755784197,4063492232,504.626.7424 | +17755784197 | 4063492232,504.626.7424 |
| 4063492232,504.626.7424 | 4063492232 | 504.626.7424 |
| 6710488141 | 6710488141 | *No value* |
| *No value* | *No value* | *No value* |

- Result of splitting into 3 columns:

| Phone number | Phone number part 1 | Phone number part 2 | Phone number part 3 |
| --- | --- | --- | --- |
| +17755784197,4063492232,504.626.7424 | +17755784197 | 4063492232 | 504.626.7424 |
| 4063492232,504.626.7424 | 4063492232 | 504.626.7424 | *No value* |
| 6710488141 | 6710488141 | *No value* | *No value* |
| *No value* | *No value* | *No value* | *No value* |

**Example 2:** The *Customer name* column needs to be split into 2 columns, with space as the delimiter.

| Customer name | Customer name part 1 | Customer name part 2 |
| --- | --- | --- |
| Joe Michael Smith | Joe | Michael Smith |
| Jane Smith | Jane | Smith |
| Anne | Anne | *No value* |
| Smith | Smith | *No value* |

**Example 3:** Address is on multiple lines and it needs to be split into three individual records. You can use `\n` as the delimiter here. See [Remarks](wrangler-step-split-column.md#remarks) for more information.

| Address | Address part 1 | Address part 2 | Address part 3 |
| --- | --- | --- | --- |
| Baker Street 221b  NW1 6XE  London | Baker Street 221b | NW1 6XE | London |

###### Remarks

- The original column is kept in the dataset by default. If you want to remove it, use the [Delete column(s) step](wrangler-step-delete-column.md).
- You can use escape sequences (`\n`, `\t`, etc.) as delimiters.
- To use a backslash itself as a delimiter, enter two backslashes.

###### See also

- [Add column step](wrangler-step-add-column.md)
- [Duplicate column step](wrangler-step-duplicate-column.md)
- [Delete column(s) step](wrangler-step-delete-column.md)
- [Rename column step](wrangler-step-rename-column.md)
- [Reorder columns step](wrangler-step-reorder-columns.md)
- [Merge columns step](wrangler-step-merge-columns.md)
- [Split column step](wrangler-step-split-column.md)
- [`split`](../developer/string-functions-ctl2.md#split) function in CTL.
