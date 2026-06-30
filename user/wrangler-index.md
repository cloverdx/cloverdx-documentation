<!-- End user’s guide > Wrangler user guide -->

## 1. Wrangler user guide

The guide introduces users to **CloverDX Wrangler**, an AI-enabled versatile data transformation tool designed to streamline the process of extracting, transforming, and loading (ETL) data.

CloverDX Wrangler allows users to connect to multiple data sources, clean and transform data, and configure outputs with minimal effort. Its user-friendly interface simplifies complex data tasks, making it accessible to both technical and non-technical users. Wrangler provides dynamic [step previews](wrangler-steps-list-basics.md#step-editing-and-step-preview) allowing users to immediately see the results of their transformation steps as they work. This feedback helps users refine their logic before applying changes to their data improving accuracy and efficiency. Wrangler is ideal for automating repeatable processes and ensuring high data quality through validation and error-handling features.

Wrangler allows you to use **Clover Assistant** - a built-in AI helper that supports you during wrangling by offering smart suggestions and guidance.

This guide begins with a [Tutorial](wrangler-tutorial.md) to help users get started quickly. Tutorial will teach you how you can create a simple job using Clover AI Assistant as well as without the Assistant.

With **Clover Assistant** integrated into the workflow, Wrangler can suggest the next best step or provide explanations directly where you need them, so you don’t lose time searching for solutions.

The [Data sources and targets](data-sources-data-targets.md) section explains how to create and select [data sources](data-sources-data-targets.md#data-sources) and create and configure [outputs](data-sources-data-targets.md#data-targets), ensuring a seamless flow from input to target. Wrangler’s [Data Catalog](data-catalog.md) is a powerful feature for searching available data sources published by your company and reviewing connector details, making it easy to integrate new data sources into your workflows. **Clover Assistant** can also help by offering suggestions when you are configuring inputs and outputs. This section also explains target mapping and [previewing target output](data-sources-data-targets.md#previewing-target-output) options that help you validate mapped output before writing data to a target.

The [Transforming data](transforming-data.md) section guides users through managing jobs on the [Jobs](transforming-data.md#jobs-screen) screen and applying transformations using the [Steps sidebar](transforming-data.md#using-steps-sidebar). You’ll learn about [data quality monitoring](transforming-data.md#data-quality-bar), [formatting](transforming-data.md#formatting-your-data), [running jobs](transforming-data.md#running-jobs-in-wrangler), and using the [expression language](transforming-data.md#how-does-wrangler-expression-language-differ-from-ctl). **Clover Assistant** can generate a summary of your job, providing a clear overview of applied transformations and outcomes.

The [Transformation steps](wrangler-steps-list.md) section details specific data manipulation tasks, including [text](wrangler-step-list-dataset-steps.md), [date](wrangler-step-list-date-steps.md), and [math transformations](wrangler-math-steps.md), [data validation](wrangler-validation-steps.md), and [anonymization](wrangler-steps-list.md) steps. Transformations are organized into blocks, which act as the main containers for steps, notes, and groups. This structure helps you keep related transformations together and maintain a clear overview of your workflow. In this section, you can also find more information about [conditions for steps and groups](step-and-group-conditions.md) which can help you manage more complex transformations.

Finally, head over to the [Frequently Asked Questions](wrangler-faq.md) page to get answers to common questions related to [choosing data source for your job](wrangler-faq.md#how-to-choose-data-source-for-your-job), [working with various data types](wrangler-faq.md#what-data-types-can-column-have), [using conditions](wrangler-faq.md#how-can-i-modify-values-based-on-a-condition), [using formulas](wrangler-faq.md#how-do-formulas-work), and more…​

![transformation editor screen](../figures/transformation-editor-screen.png)
*Figure 1. Wrangler transformation editor.*
