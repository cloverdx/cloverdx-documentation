<!-- Development > Component reference > Others > Common properties of Others components -->

### Common properties of Others components

These components serve to fulfil some tasks that have not been mentioned already. We will describe them now. They have no common properties as they are heterogeneous group.

Below is an overview of all **Others**:

| Component | Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs[[1]](common-of-others.md#common-of-others-fn01) | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [CheckForeignKey](checkforeignkey.md) | **⨯** | **⨯** | 2 | 1-2 | - | **⨯** | **⨯** | **⨯** |
| [CustomJavaComponent](genericcomponent.md) | - | - | 0-n | 0-n | - | **✓** | **⨯** | **⨯** |
| [DBExecute](dbexecute.md) | - | **⨯** | 0-1 | 0-2 | - | **⨯** | **⨯** | **⨯** |
| [HTTPConnector](httpconnector.html) | - | **⨯** | 0-1 | 0-1 | - | **⨯** | **⨯** | **✓** |
| [LookupTableReaderWriter](lookuptablereaderwriter.md) | - | **⨯** | 0-1 | 0-n | **✓** | **⨯** | **⨯** | **⨯** |
| [RESTConnector](restconnector.md) | - | **⨯** | 0-n | 0-n | - | **⨯** | **⨯** | **x** |
| [SequenceChecker](sequencechecker.md) | - | **⨯** | 1 | 1-n | **✓** | **⨯** | **⨯** | **✓** |
| [SystemExecute](sysexecute.md) | - | **⨯** | 0-1 | 0-1 | - | **⨯** | **⨯** | **⨯** |
| [WebServiceClient](webserviceclient.md) | - | **⨯** | 0-1 | 0-n | no[[2]](common-of-others.md#common-of-others-footnote2) | **⨯** | **⨯** | **⨯** |

| 1 |  The component sends each data record to all connected output ports. |
| --- | --- |

| 2 |  The component sends processed data records to the connected output ports as specified by mapping. |
| --- | --- |
