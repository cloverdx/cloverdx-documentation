<!-- Development > Component reference > Transformers > Common properties of Transformers > CTL templates for Transformers -->

#### CTL templates for Transformers

- [Partition](partition.md) requires a transformation (which can be written in both CTL and Java) unless **Partition key** or **Ranges** are defined.
  For more information about the transformation template, see [Java interface](partition.md#java-interface).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping does not need to be done, records are mapped automatically.
- [DataIntersection](dataintersection.md) requires a transformation which can be written in both CTL and Java.
  For more information about the transformation template, see [CTL templates for DataIntersection](dataintersection.md#ctl-templates-for-dataintersection).
- [Map](reformat.md) requires a transformation which can be written in both CTL and Java.
  For more information about the transformation template, see [CTL templates for Map](reformat.md#ctl-templates-for-map).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping must be defined for this port.
- [Denormalizer](denormalizer.md) requires a transformation which can be written in both CTL and Java.
  For more information about the transformation template, see [CTL templates](denormalizer.md#ctl-templates).
- [Normalizer](normalizer.md) requires a transformation which can be written in both CTL and Java.
  For more information about the transformation template, see [CTL templates for Normalizer](normalizer.md#ctl-templates-for-normalizer).
- [Rollup](rollup.md) requires a transformation which can be written in both CTL and Java.
  For more information about the transformation template, see [CTL templates for Rollup](rollup.md#ctl-templates-for-rollup).
  Remember that this component sends each record through the connected output port whose number is equal to the value returned by the transformation ([Return values of transformations](transformations.md#return-values-of-transformations)). Mapping must be defined for this port.
