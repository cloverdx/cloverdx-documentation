<!-- Administration > Upgrade -->

# Upgrade

We continually update our products and expand the support for new features to keep pace with security measures and industry standards. Upgrading is crucial to keeping your CloverDX products current and secure. To ensure a smooth upgrade, it is essential to follow best practices and thoroughly prepare for the process.

Before you begin, make sure to review our [release notes](https://support.cloverdx.com/releases/) for information on the latest changes and any compatibility updates that might impact your setup. It’s important to note that both the Designer and Server need to be updated to the same version to ensure compatibility.

For the Server upgrade, pay close attention to the [system requirements](system-requirements-for-cloverdx-server.md) for the version you are upgrading to. Verify that the version and provider of your system database are supported, as well as the combinations of your application server and JDK. Using unsupported versions or combinations may lead to functionality issues. If you’re upgrading to a newer database version, also check if the JDBC driver you use needs to be updated, as outdated drivers may cause compatibility problems.

This section provides detailed instructions for upgrading each component of our software:

- [**Designer upgrade**](upgrading-cloverdx-designer.md): Learn how to seamlessly upgrade your Designer to the latest version.
- [**Server upgrade in cloud**](common-marketplace-upgrade.md): Choose between upgrading the entire cloud architecture (see [upgrade in AWS](aws-marketplace-upgrade.md) or [upgrade in Azure](azure-marketplace-upgrade.md)) or upgrading just the clover.war file (i.e., performing [manual upgrade](upgrading-server.md)), with detailed instructions provided for each method.
- [**Server upgrade in containers**](upgrading-containers.md): Provides the steps for upgrading Server instances running in a containerized environment (i.e., Servers running in Docker or Kubernetes environments).
- [**Server manual upgrade**](upgrading-server.md): For users who prefer or require a manual approach, this section offers step-by-step instructions for upgrading the Server manually.
