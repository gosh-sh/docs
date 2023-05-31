# **Anytree**



## **Overview**


**AnyTree** — a first secure software deployment system secured by a blockchain.

Software distributed through AnyTree is secured at the source, with all its dependencies, build and compiler environments, built in isolation and cryptographically signed and timestamped, and based on **Deep SBOM** technology pioneered by GOSH.

Deep SBOM by GOSH is describing not only what, but also how something was built.
It then uses **GOSH Build** to safely build reproducible containers in an isolated environment.

On AnyTree, whatever apps developers distribute or use, are delivered exactly as they are supposed to be — what code developers didn’t write is never included.

AnyTree Packages can be downloaded from Docker Hub, GOSH Docker Desktop Extension.

AnyTree utilizes standard Docker Containers secured by GOSH Builder and is currently available as Beta on Linux and is coming soon to Windows and macOS.


##  **Quick start**

###  __for Linux__

1.**Install [**Git Remote Helper**](git-remote-helper.md#install-helper-using-the-installation-script) using the installation script**

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh/dev/install.sh | bash -s
```

[Checking](git-remote-helper.md#verifying-the-installation-result) the installation results.

2.**Install **AnyTree** using the installation script**

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh | bash -s
```

You can check installation by running:

```
which gosh
```

3.**Setup a GOSH account**

Go to GOSH-repository (`Dockerfile` should exists)

!!! note
    If you haven't GOSH-repository then  go to [GOSH Web](https://app.gosh.sh/) and [create it](gosh-web.md#create-repository)

and run:

```
gosh init
```

As a result of the onboarding process, a Gosh.yaml file will be created

4.**Now you are ready to build an image**

```
gosh build
```

As a result of execution, the hash of the created docker image will be returned and the SBOM-file ([sbom.spdx.json](https://cyclonedx.org/specification/overview/)) will be generated. 

The developer can put the generated SBOM-file in his repository for further verification.

## __Installation__

Before installing AnyTree, you must already have the [**Git Remote Helper**](git-remote-helper.md) installed.

If you have Linux, you can use these installation methods.


### __Install AnyTree using the installation script__

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh | bash -s
```

### __Install AnyTree from binary releases__

1. Follow the [link](https://github.com/gosh-sh/gosh-build-tools/releases/tag/0.1.0) and download the GOSH for the required operating system.

2. Extract files from tar-file  
(e.g. for Linux x64):

```
tar xzvf gosh-linux-amd64.tar.gz
```

3.Move binary files to any searchable path  
e.g.:

```
sudo mv gosh /usr/local/bin
```

### __Install AnyTree from source__

1. Prerequisites:

      - Rust v1.66+
      - Protobuf Compiler
      - `git`
      - `make`
      - `gcc`
      - `openssl`

2. Clone [gosh-build-tools](https://github.com/gosh-sh/gosh-build-tools.git) repository

3. Go to the `gosh-build-tools` directory

```
cd gosh-build-tools && make install
```

## **Setup a GOSH account**

Go to GOSH-repository (`Dockerfile` should exists)

!!! note
    If you haven't GOSH-repository then go to [GOSH Web](https://app.gosh.sh/) and [create it](gosh-web.md#create-repository)

and then run:

```
gosh init
```

As a result of the onboarding process, a Gosh.yaml file will be created.

<!-- 
Then you need to go through the onboarding process on GOSH using:

the [web](https://app.gosh.sh/onboarding)

or

```
gosh init
```
 -->

<!-- Log in to your GOSH account or create a [new one](gosh-web.md#create-account) -->

## **Working with AnyTree**

Prerequisites:

* Docker

### __Install image__

(WIP)

### __Build image__

AnyTree builds the Docker-container and works with the SBOM-file (creation and validation).

Gosh build can work in 2 modes:

* **with a local code base**

It is also possible to work in 2 modes: building a Docker image with the generation of an SBOM-file and building an image with subsequent validation (option `--validate`) using an existing SBOM-file.

* **with a repository on GOSH**

At the end of the build, mandatory validation is performed using the SBOM-file from the repository.

The main point is to check that the result of the builder's work corresponds to the SBOM-file stored on the blockchain.

!!! info
    For more information about the [options](anytree.md#options), see the Help section:

    ```
    gosh build --help
    ```

Before starting, you need to set docker's context in to default:

```
docker context use default
```

To work with the local code base, run:

```
gosh build
```

To work with the repository on GOSH, enter its address :
<!-- 
(a specific folder/file/comit) -->

```
gosh build [gosh://0:...]
```

As a result of execution, the hash of the created docker image will be returned and the SBOM-file ([sbom.spdx.json](https://cyclonedx.org/specification/overview/)) will be generated.


!!! info
    The developer can put the generated specification in his repository for further verification.



### __Options__

Suppress output - outputs only the resulting hash of the image or an error

```
-q, --quiet
```

Validate the result image - start checking the correctness of the built image (comparison of SBOM-files)

```
--validate
```

Socket address for the SBOM proxy server [default: 127.0.0.1:6054]

```
-s, --socket <IP:PORT>
```

Config path (in case of GOSH url context it should be relative to the root) [default: Gosh.yaml]

```
-c, --config <PATH>
```

Print help

```
-h, --help
```


<!-- ## **Examples**



### __Telepresents__ -->
