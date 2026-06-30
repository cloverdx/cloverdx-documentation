<!-- Development > Component reference > Data Quality -->

## 44. Data Quality

| [Common properties of Data Quality](common-of-data-quality.md) |
| --- |
> [!TIP]
> If you’re interested in learning more about this subject, we offer the [Data Quality course](https://academy.cloverdx.com/courses/data-quality) in our CloverDX Academy.

Some components are focused on determining and assuring the quality of your data. This group of components is called **Data Quality**.

**Data Quality** serve to perform multiple and heterogeneous tasks.

As **Data Quality** are heterogeneous group of components, they have no common properties.

We can distinguish each component of the **Data Quality** group according to the task it performs.

- [EmailFilter](emailfilter.md) validates email addresses and sends out the valid ones. Data records with invalid email addresses can be sent out through the optional second output port.
- [ProfilerProbe](profilerprobe.md) performs statistical analyses of data flowing through the component. It is a part of the **CloverDX Data Quality** package.
- [Validator](validator.md) allows you to specify a set of rules and check the validity of incoming data based on these rules. It is a part of the **CloverDX Data Quality** package.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
