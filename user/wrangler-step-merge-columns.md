<!-- End user’s guide > Wrangler user guide > Transformation steps > Data set manipulation steps > Merge columns -->

##### Merge columns

The **Merge columns** step can be used to merge data from multiple columns into a single column.

###### Parameters

- **Columns to merge**: required, select the columns to be merged in the sequence you want the values combined. You can change the column sequence by drag and dropping by the grip on the left of a column field.
- **Delimiter**: optional, specify a delimiter to be used between merged values.
  - Both single characters (including a space) and multiple characters can be used as delimiters.
  - You can also select newline or tab characters as delimiters from the dropdown list.
- **Ignore blanks**: checked by default. When checked, [empty values](wrangler-faq.md#how-do-i-work-with-empty-values-whats-the-difference-between-null-and-empty) are disregarded and not included in the merged values. This parameter is ignored when no delimiter is specified.
- **Output column name**: required, enter the name of the new column. The name defaults to *New column*.
- **Position of the output column**:
  - As the last column
  - As the first column
  - Before column
  - After column

###### Examples

| Street | City | Postal Code | Delimiter | Ignore blanks | Result |
| --- | --- | --- | --- | --- | --- |
| Baker Street 221b | NW1 6XE | London | (No delimiter specified) | Any | Baker Street 221bNW1 6XELondon |
| Baker Street 221b | *No Value* | London | (No delimiter specified) | Any | Baker Street 221bLondon |
| Baker Street 221b | NW1 6XE | London | , | Any | Baker Street 221b,NW1 6XE,London |
| Baker Street 221b | *No Value* | London | , | Yes (checked) | Baker Street 221b,London |
| Baker Street 221b | *No Value* | London | , | No (unchecked) | Baker Street 221b,,London |
| Baker Street 221b | "    " (4 spaces) [[1]](wrangler-step-merge-columns.md#wrangler-step-merge-columns-fn1) | London | , | Any | Baker Street 221b,    ,London |
| Baker Street 221b | NW1 6XE | London | \n [[2]](wrangler-step-merge-columns.md#wrangler-step-merge-columns-fn2) | Any | ``` Baker Street 221b NW1 6XE London ``` |
| Baker Street 221b | NW1 6XE | London | \\ [[3]](wrangler-step-merge-columns.md#wrangler-step-merge-columns-fn3) | Any | Baker Street\221b\NW1 6XE\London |

| 1 | Spaces are not considered an empty value. |
| --- | --- |

| 2 | You can use escape sequences (`\n`, `\t`, etc.) as delimiters. |
| --- | --- |

| 3 | To use a backslash itself as a separator, enter two backslashes. |
| --- | --- |

###### See also

- [Add column step](wrangler-step-add-column.md)
- [Delete column(s) step](wrangler-step-delete-column.md)
- [Duplicate column step](wrangler-step-duplicate-column.md)
- [Rename column step](wrangler-step-rename-column.md)
- [Reorder columns step](wrangler-step-reorder-columns.md)
- [Split column step](wrangler-step-split-column.md)
