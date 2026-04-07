<!-- Development > Component reference > Readers > Common properties of Readers > Java interfaces for Readers -->

#### Java interfaces for Readers

- [DataGenerator](datagenerator.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interface](datagenerator.md#java-interface).
  Remember that this component allows sending of each record through a connected output port whose number equals the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping must be defined for such a port.
- [JMSReader](jmsreader.md) allows optionally a transformation which can be written in Java only.
  For more information about the interface, see [Java interfaces for JMSReader](jmsreader.md#java-interfaces-for-jmsreader).
  Remember that this component sends each record through all of the connected output ports. Mapping does not need to be defined.
- [MultiLevelReader](multilevelreader.md) requires a transformation which can only be written in Java.
  For more information, see [Java interfaces for MultiLevelReader](multilevelreader.md#java-interfaces-for-multilevelreader).
