<!-- Development > Component reference > Data Quality > Common properties of Data Quality components -->

### Common properties of Data Quality components

The **Data Quality** is a group of components performing various tasks related to quality of your data - determining information about the data, finding and fixing problems, etc. These components have no common properties as they perform a wide range of tasks.

The ProfilerProbe and Validator components are a part of the **CloverDX Data Quality** package.

Below is an overview of all **Data Quality** components:

| Component | Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs[[1]](common-of-data-quality.md#common-of-data-quality-footnote1) | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [EmailFilter](emailfilter.md) | - | **⨯** | 1 | 0-2 | **⨯** | **⨯** | **⨯** | **✓** |
| [ProfilerProbe](profilerprobe.md) | - | **⨯** | 1 | 1-n | **✓** | **⨯** | **✓** | **✓** |
| [Validator](validator.md) | - | **⨯** | 1 | 1-2 | **⨯** | **⨯** | **✓** | **⨯** |

| 1 |  The component sends each data record to all connected output ports. |
| --- | --- |

See [Data Quality](data-quality.md) next.
