# **AnyTree Firewall for Telepresence**



## **Overview**



The GOSH AnyTree Firewall integration with Telepresence is designed to make sure everything developed with Telepresence for Docker will be identically reproduced with every build, regardless of other changes made in the development process. The integration tool provides an additional security measure, so  developers can build revolutionary software faster and with confidence. 

Part of the GOSH AnyTree Firewall is the ‘Deep SBOM’ -  a tool describing not only what, but also how something was built, and uses GOSH Build to safely build reproducible containers in an isolated environment.




## **Quick start**

###  __for Linux and WSL__

1.**Install [**Git Remote Helper**](git-remote-helper.md#install-helper-using-the-installation-script) using the installation script**

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh/dev/install.sh | bash -s
```

[Checking](git-remote-helper.md#verifying-the-installation-result) the installation results.

2.**Install **GOSH AnyTree** using the installation script**

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh | bash -s
```

You can check installation by running:

```
gosh anytree --version
```

3.**Install......**

4.**Using ........**
<!-- 
TODO
change 
-->

Specify the address of the repository from which you want to perform the installation:

```
gosh anytree install [options] gosh://0:1fa4...4af1/example_dao/example_repo_name
```

or you can specify a commit or branch (else there will be a default branch):

```
gosh anytree install [options] gosh://0:1fa4...4af1/example_dao/example_repo_name#commit_or_branch_hash:dir/in/git/repo
```

The result of the execution will be what is described in your Dockerfile.



## __Installation__



Before installing AnyTree, you must already have the [**Git Remote Helper**](git-remote-helper.md) installed.

If you have Linux or WSL, you can use these installation methods.


### __Install GOSH AnyTree__


#### __using the installation script__

```
wget -O - https://raw.githubusercontent.com/gosh-sh/gosh-build-tools/dev/install.sh | bash -s
```

#### __from binary releases__

1.Follow the [link](https://github.com/gosh-sh/gosh-build-tools/releases/tag/0.1.0) and download GOSH for the required operating system.

2.Extract files from tar-file  
for example, for Linux x64, run:

```
tar xzvf gosh-linux-amd64.tar.gz
```

3.Move binary files to any searchable path  
for example:

```
sudo mv gosh /usr/local/bin
```

#### __from source__

1. Prerequisites:

      - Rust v1.66+
      - Protobuf Compiler
      - `git`
      - `make`

2. Clone [gosh-build-tools](https://github.com/gosh-sh/gosh-build-tools.git) repository

3. Go to the `gosh-build-tools` directory

```
cd gosh-build-tools && make install
```



### **Install telepresence**



## **Working with AnyTree**