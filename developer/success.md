<!-- Development > Component reference > Job Control > Success -->

### Success

![Success 64x64](../figures/Success-64x64.png)

| [Short description](success.md#short-description) |
| --- |
| [Ports](success.md#ports) |
| [Success attributes](success.md#success-attributes) |
| [Details](success.md#details) |
| [See also](success.md#see-also) |

#### Short description

**Success** is a successful endpoint in a jobflow.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| none | 0-1 | 0 | **⨯** | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0-1 | **✓** | For received tokens | Any |

#### Success attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Message | no | Text message to log for each incoming token. | text |
| Mapping | no | Mapping is used for dynamic assembling of a log message. Moreover, dictionary content can be changed as well. See [Details](success.md#details). |  |

#### Details

**Success** is a successful endpoint in a jobflow. Tokens that flow into the component are not processed anymore - they are considered to be successfully processed within the jobflow. The component can serve as a visual marker of success in a jobflow.

The component can log a message and set contents of a dictionary - it is similar to the [Fail](fail.md) component.

##### Mapping details

Mapping in the **Success** component is generally used for two purposes:

- Assembling of a log message from an incoming record.
- Populating a dictionary content from an incoming record.
  > [!NOTE]
  > Only output dictionary entries can be changed.

A log message compiled by the mapping has the highest priority. If the mapping does not set 'message', the message from the component attribute is used instead. If no message is set via the attribute or mapping, nothing is logged.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
