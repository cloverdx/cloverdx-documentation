<!-- Development > Component reference > Joiners > Common properties of Joiners > Slave duplicates -->

#### Slave duplicates

In **Joiners**, sometimes more slave records have the same values of corresponding fields of **Join key**. These slaves are called duplicates. If such duplicate slave records are allowed, all of them are parsed and joined with a master record if they match any. If the duplicates are not allowed, only one of them or at least some of them is/are parsed (if they match any master record) and the others are discarded.

Different **Joiners** allow to process slave duplicates in a different way. Here is a brief overview of how these duplicates are parsed and what can be set in these components or other tools:

- The **Allow slave duplicates** attribute is included in the following **Joiners** (It can be set to `true` or `false`.):
  - **ExtHashJoin**
    The default value is `false`. Only the **first** record is processed, the others are discarded.
  - **ExtMergeJoin**
    The default value is `true`. If switched to `false`, only the **last** record is processed, the rest is discarded.
  - **RelationalJoin**
    The default value is `false`. Only the **first** record is processed, the rest is discarded.
- The **SQL query** attribute is included in **DBJoin**. **SQL query** allows to specify the exact number of slave duplicates explicitly.
- **LookupJoin** parses slave duplicates according to the setting of used lookup table in the following way:
  - **Simple lookup table** also has the **Allow key duplicate** attribute. Its default value is `true`. If you uncheck the checkbox, only the **last** record is processed, the others are discarded.
  - **DB lookup table** allows to specify the exact number of slave duplicates explicitly.
  - **Range lookup table** does not allow slave duplicates. Only the **first** slave record is used, the rest is discarded.
  - **Persistent lookup table** can work in two modes: with and without slave duplicates. See [Persistent lookup table](lookup-tables.md#persistent-lookup-table).
  - **Aspell lookup table** allows that all slave duplicates are used. No limitation of the number of duplicates is possible.
