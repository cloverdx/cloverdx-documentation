<!-- Development > Component reference > AI Components -->

## 40. AI Components

| [Common properties of AI components](common-of-ai-components.md) |
| --- |
> [!NOTE]
> AI components are currently in the **incubation phase**. Although they are available for use, they are under active development and may be subject to changes. We welcome feedback and encourage users to explore their capabilities.

Our **AI-based transformation components** give you the ability to seamlessly integrate machine learning into your transformation graphs.

**What do the AI components do?**

Think of AI components as wrappers around models. A choice of a model determines the capabilities of the components – some models detect positive/negative sentiment, some can detect PIIs, others can tokenize and classify pre-trained entities in your data. Typically, larger models are more accurate yet take longer to process while smaller, dedicated models can provide much higher speeds with acceptable levels of accuracy.

**AI models hosted locally**

While there are exceptions ([AIClient](aiclient.md)), most of the components are executing pre-trained AI models hosted locally, under your full control on your CloverDX Server – either on your own hardware or in a cloud environment of your choice — with support for either hardware acceleration through GPUs or fallback to CPU. This flexibility ensures that you retain complete control over the execution environment and location of your data, allowing you to meet strict requirements for data privacy, security, and regulatory compliance.
> [!TIP]
> For customers looking to explore the capabilities of AI components, the setup can be accelerated by using the [official Docker image for AI workloads](https://hub.docker.com/r/cloverdx/cloverdx-server-ai). This image includes a pre-configured CloverDX Server as well as drivers and additional software needed to take advantage of hardware acceleration of AI workloads. The image must be deployed on a machine with NVIDIA GPU to use the GPU acceleration.

**Which models are available?**

Models are not distributed as part of the core product and need to be downloaded and deployed to CloverDX Server by the admin before use. You can provide your own model (some configuration required – only for experienced users) or choose from a curated set of free, ready-to-use models available in our online [CloverDX Marketplace](https://marketplace.cloverdx.com) (recommended).

**Sending data to third-party service providers**

Beware, some components ([AIClient](aiclient.md)) do not conform to the “hosted locally” paradigm and use external third-party online services to process your data. Keep this in mind when choosing which component you want to use. While third-party services provide much more powerful AI capabilities, you are responsible for making sure their privacy and security policies match your requirements.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
