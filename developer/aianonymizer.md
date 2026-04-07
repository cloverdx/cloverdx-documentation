<!-- Development > Component reference > AI Components > AIAnonymizer -->

### AIAnonymizer

![AIAnonymization 64x64](../figures/AIAnonymization-64x64.png)

| [Short description](aianonymizer.md#short-description) |
| --- |
| [Ports](aianonymizer.md#ports) |
| [Metadata](aianonymizer.md#metadata) |
| [AIAnonymizer attributes](aianonymizer.md#aianonymizer-attributes) |
| [Compatibility](aianonymizer.md#compatibility) |
| [See also](aianonymizer.md#see-also) |
> [!NOTE]
> This component is currently in the **incubation phase**. Although it is available for use, it is under active development and may be subject to changes. We welcome feedback and encourage users to explore its capabilities.

#### Short description

The **AIAnonymizer** lets you run a token classification model (preferably a PII detection model such as Piiranha - see [CloverDX Marketplace](https://marketplace.cloverdx.com)) and mask identified tokens in the output.

This component behaves just like [AITokenClassifier](tokenclassifier.md) but with the added functionality of masking (anonymizing) tokens identified by the model above configured thresholds.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1 | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 1 | **✓** | The text(s) to classify | At least one `string` field |
| Output | 1 | **✓** | Copy of the input data with anonymized texts + token classification result | Any |

#### Metadata

**AIAnonymizer** propagates input metadata to output.

#### AIAnonymizer attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| **Model** |  |  |  |
| Server model |  | Recommended: Use a model installed as a library on the CloverDX Server. Check [CloverDX Marketplace](https://marketplace.cloverdx.com) for available ready-to-use models. This is a more convenient alternative to **Classification model directory**. |  |
| Classification model directory |  | Path to the [machine learning model directory](libraries-dev.md#machine-learning-models). It is required unless **Server model** is defined. |  |
| Model name | no | A read-only field displaying name defined in model configuration files (if available). |  |
| Device | yes | The device to run the model – either processor (CPU) or graphics card (GPU). You must set the device the model is designed for. GPU models are much faster but you need a specialized hardware to use them. | CPU (default) \| GPU |
| Model arguments | no | Configuration arguments for the model. See documentation of your particular model. |  |
| Tokenizer arguments | no | Configuration arguments for the tokenizer. See documentation of your particular model. |  |
| Translator arguments | no | Configuration arguments for the translator. See documentation of your particular model. |  |
| **Input / output parameters** |  |  |  |
| Fields to anonymize | yes | List of `string` fields to be classified and anonymized. |  |
| Anonymize classes and thresholds |  | List of token classes who shall be anonymized. The classes are model-dependent; you can use only some of them, but you cannot add classes unknown to the model. The thresholds define the minimum score at which the particular token is anonymized – it is masked if at least one class reaches its threshold. |  |
| Masking type | yes | Determines which anonymization method is applied: character-level masking using the mask character, or full-string redaction using the redact string. |  |
| Mask character | no | The character used for masking characters of the anonymized tokens. |  |
| Redact string | no | The static replacement value that substitutes the entire anonymized string. |  |
| Anonymization information | no | An output field which will store the analysis results. It must be of *variant* type. If the field already contains some analysis, the analyses are merged, so that you can concatenate several AI components and use their combined output. |  |
| Batch size | no | Number of records processed by model together. | an integer number |

#### Compatibility

| Version | Compatibility notice |
| --- | --- |
| 7.1.0 | AIAnonymizer is available since CloverDX version 7.1. |

#### See also

| [AITokenClassifier](tokenclassifier.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
