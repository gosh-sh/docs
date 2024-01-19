# **AnyTree Firewall for Telepresence**



## **Overview**



The GOSH AnyTree Firewall integration with [**Telepresence**](https://www.getambassador.io/products/telepresence){:target="_blank"} is designed to make sure everything developed with Telepresence for Docker will be identically reproduced with every build, regardless of other changes made in the development process. The integration tool provides an additional security measure, so  developers can build software faster and with confidence.

Part of the GOSH AnyTree Firewall is the ‘Deep SBOM’ -  a tool describing not only what, but also how something was built, and uses [**GOSH Anytree Builder**](anytree.md#quick-start-gosh-anytree-builder) to safely build reproducible containers in an isolated environment.

GOSH AnyTree Firewall is currently in Beta testing stages on Linux only, but will be available on other platforms and Docker Desktop in the near future.



## **Quick start**


###  __for Linux__


1. **Install [**Git Remote Helper**](git-remote-helper.md#installation) using the installation script**

    ``` sh
    wget -O - \
      https://raw.githubusercontent.com/gosh-sh/gosh/dev/install.sh \
      | bash -s
    ```

    [Checking](git-remote-helper.md#verifying-the-installation-result) the installation results.

2. **Install [**GOSH AnyTree**](anytree.md#installation) using the installation script**

    ``` sh
    wget -O - \
      https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh \
      | bash -s
    ```

    You can check installation by running:

    ``` sh
    gosh anytree --help
    ```

3. **Install [Kubernetes](https://kubernetes.io){:target="_blank"} with [Telepresence the Traffic Manager](https://www.getambassador.io/docs/telepresence/latest/quick-start){:target="_blank"}**


    !!! Warning
        We need to return docker's context to default.

        ```
        docker context use default
        ```

        To see all available docker's contexts type:

        ```
        docker context list
        ```

4. **Start Telepresence with AnyTree Firewall**

    ``` {.sh .no-copy}
    telepresence intercept [OPTIONS] --docker-build \
      gosh://0:0d5...e92c/<your_dao>/<your_repo>#<commit_or_branch_or_tag> \
      <k8s_pod_name>
    ```
