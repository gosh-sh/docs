# **AnyTree**



## **Overview**



**AnyTree** — the first software deployment system secured by the blockchain.


AnyTree has 2 subcommands:

<!-- AnyTree can be used as a builder and also as an installer. -->

* [build](anytree.md#gosh-anytree-builder)
* [install](anytree.md#gosh-anytree-installer)


Software distributed through [**GOSH AnyTree Installer**](anytree.md#install-image) is secured at the source, with all its dependencies, build and compiler environments, built in isolation and cryptographically signed and timestamped, and based on **Deep SBOM** technology pioneered by GOSH.

<!-- 
Deep SBOM by GOSH is describing not only what, but also how something was built.
Then **GOSH AnyTree Builder** uses it to safely build reproducible containers in an isolated environment. -->

[**GOSH AnyTree Builder**](anytree.md#build-image) creates reproducible containers in an isolated environment. Also, the result of his work will be the creation of a `SBOM file`. It is describing not only what, but also how something was built.


On AnyTree, whatever apps developers distribute or use, are delivered exactly as they are supposed to be — what code developers didn’t write is never included.

AnyTree secures the delivery of any package you use today. AnyTree works with almost any package manager, user or server applications (including PIP, NPM, Brew, Maven...).


AnyTree utilizes standard Docker Containers secured by **GOSH AnyTree Builder** and is currently available as Beta on Linux and is coming soon to Windows and macOS.



## **Quick start**


<!-- ### **GOSH AnyTree Builder** -->
### **Building an image**

!!! info
    The current version of AnyTree only supports Linux.


<!-- #### __[for Linux]__ -->


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

3. **Setup a GOSH project**

    You need a GOSH repository.  
    If you haven't used a GOSH-repository you can upload your github-repository to GOSH through [onboarding](https://app.gosh.sh/onboarding) or create a [GOSH-account](https://app.gosh.sh/) and [create a new one](gosh-web.md#create-repository).

    Go to your GOSH-repository

    !!! Warning
        There should already exist a working `Dockerfile` in it.

    and run:

    ``` sh
    gosh init
    ```

    As a result of the onboarding process a `Gosh.yaml` file will be created.

    ``` yaml title="Gosh.yaml"
    ---
    dockerfile:
      path: Dockerfile
    tag: your-image-tag

    ```

4. **Now you are ready to build an image**

    Run:
    ``` sh
    gosh anytree build
    ```

    As a result of execution, the hash of the created docker image will be returned and the SBOM-file `sbom.spdx.json` will be generated. 

    The SBOM-file follows [CycloneDX object model](https://cyclonedx.org/specification/overview/).


    The developer can put the generated SBOM-file in his repository for further verification.

    !!! Tip
        Place the SBOM-file in the same folder where `GOSH.yaml` is located.



<!-- ### **GOSH AnyTree Installer** -->
### **Installing the image**


<!-- #### **for Linux** -->


1. **Install [**Git Remote Helper**](git-remote-helper.md#install-helper-using-the-installation-script) using the installation script**

    ``` sh
    wget -O - \
    https://raw.githubusercontent.com/gosh-sh/gosh/dev/install.sh \
    | bash -s
    ```

    [Checking](git-remote-helper.md#verifying-the-installation-result) the installation results.

2. **Install **GOSH AnyTree** using the installation script**

    ``` sh
    wget -O - \
    https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh \
    | bash -s
    ```

    You can check installation by running:

    ``` sh
    gosh anytree --help
    ```

3. **Using GOSH AnyTree Installer**

    Specify the address of the repository from which you want to perform the installation:

    ``` sh
    gosh anytree install [options] \
    gosh://0:1fa4...4af1/example_dao/example_repo_name
    ```

    or you can specify a commit or branch (else there will be a default branch):

    ``` sh
    gosh anytree install [options] \
    gosh://0:1fa4...4af1/example_dao/example_repo_name#commit_or_branch_hash:dir/in/git/repo
    ```

    The result of the execution will be what is described in your Dockerfile.



## __Installation AnyTree__



Before installing AnyTree, you must already have the [**Git Remote Helper**](git-remote-helper.md) installed.

If you have Linux you can use these installation methods:


### **Install AnyTree using the installation script**


``` sh
wget -O - \
https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh \
| bash -s
```


### __Install AnyTree from binary releases__


1. Follow the [link](https://github.com/gosh-sh/gosh-build-tools/releases/tag/0.1.1) and download GOSH AnyTree for the required operating system.

2. Extract files from tar-file

    for example, for Linux x64, run:

    ``` sh
    tar xzvf gosh-linux-amd64.tar.gz
    ```

3. Move binary files to any searchable path  
    for example:

    ``` sh
    sudo mv gosh /usr/local/bin
    ```


### __Install AnyTree from source__


1. Prerequisites:

      - Rust v1.66+
      - Protobuf Compiler
      - `git`
      - `make`

2. Clone [gosh-build-tools](https://github.com/gosh-sh/gosh-build-tools.git) repository

3. Go to the `gosh-build-tools` directory

    ``` sh
    cd gosh-build-tools && make install
    ```



## **Setup a GOSH project**



You need a GOSH repository.  
If you haven't used a GOSH-repository you can upload your github-repository to GOSH through [onboarding](https://app.gosh.sh/onboarding) or create a [GOSH-account](https://app.gosh.sh/) and [create a new one](gosh-web.md#create-repository).

Go to your GOSH-repository

!!! Warning
    There should already exist a working `Dockerfile` in it.

and run:

``` sh
gosh init
```

As a result of the onboarding process a `Gosh.yaml` file will be created.

``` yaml title="Gosh.yaml"
---
dockerfile:
    path: Dockerfile
tag: your-image-tag

```



## **Working with AnyTree**



Prerequisites:

* Docker

### __Building image__


AnyTree builds the Docker-image and works with the SBOM-file (creation and validation).

Before starting set docker's context to default:

``` sh
docker context use default
```

!!! info
    For more information about the [`build` options](anytree.md#build), see the Help section:

    ``` sh
    gosh anytree build --help
    ```

<u>GOSH AnyTree Builder can work in 2 modes: </u>

* **with a local code base**

To work with the local code base, run:

``` sh
gosh anytree build [options]
```

After making changes to the codebase, you can check the correctness of the SBOM-file by running:

``` sh
gosh anytree build --validate
```

!!! info
    Instead of creating an SBOM-file, a check will be run to make sure that the new SBOM-file matches the last generated file.


* **with a repository on GOSH**

At the end of the build, mandatory validation is performed using the SBOM-file from the repository.

The main point is to check that the result of the builder's work corresponds to the SBOM-file stored on the blockchain.

To work with the repository on GOSH, specify its address:

``` sh
gosh anytree build [options] \
  gosh://0:1fa4...4af1/example_dao/example_repo_name
```

or you can specify a commit or branch (else there will be a default branch):

``` sh
gosh anytree build [options] \
  gosh://0:1fa4...4af1/example_dao/example_repo_name#commit_or_branch_hash:dir/in/git/repo
```

As a result of execution, the hash of the created docker image will be returned and the SBOM-file ([`sbom.spdx.json`](https://cyclonedx.org/specification/overview/)) will be generated.


!!! info
    The developer can put the generated specification in his repository for further verification.

### __Installing image__

The GOSH AnyTree Installer does not generate an SBOM file. It is assumed that the SBOM file already exists.

Its main tasks is to download the image, check the correctness of the SBOM file and install everything as specified in the docker file.

So, first specify the address of the repository from which you want to perform the installation:

``` sh
gosh anytree install [options] \
  gosh://0:1fa4...4af1/example_dao/example_repo_name
```

or you can specify a commit or branch (else there will be a default branch):

``` sh
gosh anytree install [options] \
  gosh://0:1fa4...4af1/example_dao/example_repo_name#commit_or_branch_hash:dir/in/git/repo
```

During the installation process, the SBOM-file will be checked.

And as a result of the installation, an artifact will appear that will be installed on your computer.

!!! info
    For more information about the [`install` options](anytree.md#install), see the Help section:

    ``` sh
    gosh anytree install --help
    ```


<!-- 
TODO 
for example install AnyTree for using Telepresence or another case
-->


### __Options__


#### __build__

Suppress output - outputs only the resulting hash of the image or an error

``` sh
-q, --quiet
```

Validate the result image - start checking the correctness of the built image  
(comparison of SBOM-files)

``` sh
--validate
```

Socket address for the SBOM proxy server  
[default: 127.0.0.1:6054]

``` sh
-s, --socket <IP:PORT>
```

Config path (in case of GOSH url context it should be relative to the root)  
[default: `Gosh.yaml`]

``` sh
-c, --config <PATH>
```

Print help

``` sh
-h, --help
```

#### __install__

Socket address for the SBOM proxy server [default: 127.0.0.1:6054]

``` sh
-s, --socket <IP:PORT>
```

Config path (in case of GOSH url context it should be relative to the root) [default: `Gosh.yaml`]

``` sh
-c, --config <PATH>
```

Print help

``` sh
-h, --help
```


 
### __Known issues__

We would like to bring to your attention a memory limitation concern that has been identified when working with large repositories. Under certain circumstances, you might encounter memory depletion issues which could potentially affect your work efficiency and system performance. We deeply apologize for any inconvenience this may cause.

Rest assured, we are committed to promptly resolving this issue. Our dedicated team of developers has already initiated efforts to address this, with an anticipated resolution targeted within the next two weeks. We appreciate your patience and understanding as we continue to enhance and streamline our services.


### __Contact us__

If you have any questions or issues using GOSH AnyTree, please email us at [help@gosh.sh](mailto:help@gosh.sh)

