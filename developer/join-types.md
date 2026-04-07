<!-- Development > Component reference > Joiners > Common properties of Joiners > Join types -->

#### Join types

**Joiners** can work under the following three processing modes:

- **Inner join**
  In this processing mode, only master records in which values of **Join key** fields are equal to values of their slave counterparts are processed and sent out through the output port for joined records.
  Unmatched master records can be sent out through the optional output port for master records without a slave (in **ExtHashJoin**, **ExtMergeJoin**, **LookupJoin** or **DBJoin** only).
- **Left outer join**
  In this processing mode, all master records are joined and forwarded to the output. Master records with no corresponding item in a lookup table have null values in fields containing data from the lookup table.
- **Full outer join**
  In this processing mode, all master and slave records are processed and sent out through the output port for joined records, regardless of whether the values of **Join key** fields are equal to the values of their slave counterparts or not.
> [!IMPORTANT]
> **Full outer join** mode is not allowed in **LookupJoin** and **DBJoin**.
> [!NOTE]
> Null values
> **Joiners** parse each pair of records (master and slave) in which the same fields of the **Join key** attribute have `null` values as if these `nulls` were different. Thus, these records do not match one another in such fields and are not joined.
