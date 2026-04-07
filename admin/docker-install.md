<!-- Administration > Installation > Server installation > Docker and Kubernetes deployments -->

### Docker and Kubernetes deployments

Since version 6.4, **CloverDX** offers an **official Docker image** for simplified and streamlined deployment of **CloverDX Server**. This image provides a containerized environment pre-configured with:

- Good defaults: Out-of-the-box settings suitable for most use cases.
- Recommended environment: Optimized configuration for running **CloverDX Server** efficiently.

Key benefits of using the Docker image:

- Faster deployment and upgrade: Reduces manual configuration steps, allowing quicker setup of **CloverDX Server.**
- Portability: Ensures consistent environment across different systems.

For a quick overview of the **CloverDX Docker image**, visit our **Docker Hub site**: [https://hub.docker.com/r/cloverdx/cloverdx-server](https://hub.docker.com/r/cloverdx/cloverdx-server).

For a direct link to the image with detailed information and configuration options, visit the official **CloverDX Server Docker image repository** on GitHub: [https://github.com/cloverdx/cloverdx-server-docker](https://github.com/cloverdx/cloverdx-server-docker).

This Docker image can also be deployed in **Kubernetes environments**. You can find examples of deployments in Kubernetes with deployment steps in the [GitHub](https://github.com/cloverdx/cloverdx-server-docker) repository in the `examples/kubernetes` directory, where there are two sample deployments, one for a standalone CloverDX Server and one for a 3-node cluster environment.
> [!TIP]
> For customers looking to explore the capabilities of [AI components](../developer/ai-components.md), the setup can be accelerated by using the [official Docker image for AI workloads](https://hub.docker.com/r/cloverdx/cloverdx-server-ai). This image includes a pre-configured CloverDX Server as well as drivers and additional software needed to take advantage of hardware acceleration of AI workloads. The image must be deployed on a machine with NVIDIA GPU to use the GPU acceleration.
