<!-- Development > Job elements > Metadata > Changing and defining delimiters -->

### Changing and defining delimiters

There are three types of delimiter: **record delimiter**, **default field delimiter** and **field delimiter.**

Delimiters can be seen and edited in **Metadata Editor**. They are displayed in the fourth column (**Delimiter** column) of the **Record** pane.

If the delimiter in this **Delimiter** column of the **Record** pane is grayish, this means that the default delimiter is used. If you look at the **Delimiter** row in the **Details** pane on the right side from the **Record** pane, you will see that this row is empty.
> [!NOTE]
> Remember that the first row of the **Record** pane displays the information about the record as a whole instead of about its fields. Field numbers, field names, their types, delimiters and/or sizes are displayed starting from the second row. For this reason, if you click the first row of the **Record** pane, information about the whole record instead of any individual field will be displayed in the **Details** pane.
> [!IMPORTANT]
> - **Multiple delimiters**
>   If you have records with multiple delimiters (for example: `John;Smith\30000,London|Baker Street`), you can specify default delimiter as follows:
>   Type all these delimiters as a sequence separated by `\\|`. The sequence does not contain white spaces.
>   For the example above there would be `,\\|;\\||\\|\\` as the default delimiter. Note that double backslashes stand for single backslash as delimiter.
>   The same can be used for any other delimiter, also for record delimiter and/or non-default delimiter.
>   For example, record delimiter can be the following:
>   `\n\\|\r\n`
>   Also, remember that you can have delimiter as a part of field value of flat files if you set the **Quoted string** attribute of **FlatFileReader** to `true` and surround the field containing such delimiter by quotes. For example, if you have records with comma as field delimiter, you can process the following as one field:
>   `"John,Smith"`
> - **CTL expression delimiters**
>   If you need to use any non-printable delimiter, you can write it down as a CTL expression. For example, you can type the following sequence as the delimiter in your metadata:
>   `\u0014`
>   Such expressions consist of the Unicode `\uxxxx` code with no quotation marks around. Please note that each backslash character '\' contained in the input data will actually be doubled when viewed. Thus, you will see "\\" in your metadata.
> [!IMPORTANT]
> **Java-style Unicode expressions**
>
> Remember that since version 3.0, you can also use the Java-style Unicode expressions (except in URL attributes).
>
> You may use one or more Java-style Unicode expressions (for example, like this one): `\u0014`.
>
> Such expressions consist of series of the `\uxxxx` codes of characters.
>
> They may also serve as delimiter (like CTL expression shown above, without any quotes):
>
> `\u0014`

#### Changing record delimiter

**Record Delimiter** can be changed in **Details pane**:

- Click the first row in the **Record** pane of the **Metadata Editor**.
  After that, there will appear record properties in the **Details** pane. Among them, there will be the **Record delimiter** property. Change this delimiter for any other value.
  Such new value of the record delimiter will appear in the last row of the **Record** pane instead of the previous value of record delimiter. It will again be displayed grayish.
> [!IMPORTANT]
> Remember that if you tried to change the record delimiter by changing the value displayed in the last row of the **Record** pane, you would not change the record delimiter. This way, you would only define other delimiter following the last field and preceding the record delimiter.

#### Changing default (field) delimiter

If you want to change the default delimiter for any other value, you can do it in one of the following two ways:

- **In Record Pane**
  Click the **Delimiter** column of the first row in the **Record** pane of the **Metadata Editor**. After that, you only need to replace the value of this cell by any other value.
  Change this delimiter for any other value.
  Such new value will appear both in the **Default delimiter** row of the **Details** pane and in the rows of the **Record** pane where default delimiter has been used instead of the previous value of such default delimiter. These values will again be displayed grayish.
- **In Details Pane**
  Click any column of the first row in the **Record** pane of the **Metadata Editor**. After that, record properties appear in the **Details** pane. Among them is the **Default delimiter** property. Change this delimiter for any other value.
  Such new value of default delimiter will appear in the rows of the **Record** pane where default delimiter has been used instead of the previous value of default delimiter. These values will again be displayed grayish.

#### Defining non-default delimiter for a field

Non-default (or field-specific) delimiter is a delimiter specific to particular field. If all fields are separated by the same delimiter, use default field delimiter instead.

There are two ways to set up field-specific delimiter:

- **In Record Pane**
  Click **Delimiter** column of a field in **Record** pane and replace it by required character(s) from the list.
  Such new character(s) will override the default field delimiter and will be used as the delimiter between the field and following field in the same row.
  The non-default delimiter will also be displayed in the **Delimiter** row of the **Details** pane which was empty if default delimiter had been used.
- **In Details Pane**
  Click any column of the row of field just before the delimiter in the **Record** pane of the **Metadata Editor**.
  Properties of the field appear in the **Details** pane on the right side. There is the **Delimiter** property. If it is empty, default delimiter is used. Type desired value to **Delimiter** property.
  New character(s) will override the default delimiter and will be used as the delimiter between the field in the same row and the field in the following row.
  To change back to default delimiter just delete the value of **Delimiter** in the **Details** pane.
> [!IMPORTANT]
> Remember that if you defined any other delimiter for the last field in any of the two ways described now, such non-default delimiter would not override the record delimiter. It would only append its value to the last field of the record and would be located between the last field and before the record delimiter.
