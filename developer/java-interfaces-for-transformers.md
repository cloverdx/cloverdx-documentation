<!-- Development > Component reference > Transformers > Common properties of Transformers > Java interfaces for Transformers -->

#### Java interfaces for Transformers

- [Partition](partition.md) requires a transformation (which can be written in both CTL and Java) unless **Partition key** or **Ranges** are defined.
  For more information about the interface, see [Java interface](partition.md#java-interface).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping does not need to be done, records are mapped automatically.
- [DataIntersection](dataintersection.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interfaces for DataIntersection](dataintersection.md#java-interfaces-for-dataintersection).
- [Map](reformat.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interfaces for Map](reformat.md#java-interfaces-for-map).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping must be defined for such port.
- [Denormalizer](denormalizer.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interface](denormalizer.md#java-interface).
- [Normalizer](normalizer.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interface](normalizer.md#java-interface).
- [Rollup](rollup.md) requires a transformation which can be written in both CTL and Java.
  For more information about the interface, see [Java interface](rollup.md#java-interface).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping must be defined for such port.
