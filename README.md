# Kyma CLI

## Overview

Kyma CLI is a command line tool which supports [Kyma](https://github.com/kyma-project/kyma) developers. It provides a set of commands you can use to install, manage, and test Kyma. 

## Prerequisites

Kyma CLI requires the following software:
- [kubectl](https://github.com/kubernetes/kubectl) 
- [Minikube](https://github.com/kubernetes/minikube) 

## Installation

Use the following options to install Kyma CLI from the latest release. 

### Homebrew (macOS)
To install Kyma CLI using Homebrew, run:
```
brew install kyma-cli
```

### macOS
To install Kyma CLI on macOS, run:

```
curl -Lo kyma.tar.gz "https://github.com/kyma-project/cli/releases/download/$(curl -s https://api.github.com/repos/kyma-project/cli/releases/latest | grep tag_name | cut -d '"' -f 4)/kyma_Darwin_x86_64.tar.gz" \
&& mkdir kyma-release && tar -C kyma-release -zxvf kyma.tar.gz && chmod +x kyma-release/kyma && sudo mv kyma-release/kyma /usr/local/bin \
&& rm -rf kyma-release kyma.tar.gz
```

### Linux
To install Kyma CLI on Linux, run:

```
curl -Lo kyma.tar.gz "https://github.com/kyma-project/cli/releases/download/$(curl -s https://api.github.com/repos/kyma-project/cli/releases/latest | grep tag_name | cut -d '"' -f 4)/kyma_Linux_x86_64.tar.gz" \
&& mkdir kyma-release && tar -C kyma-release -zxvf kyma.tar.gz && chmod +x kyma-release/kyma && sudo mv kyma-release/kyma /usr/local/bin \
&& rm -rf kyma-release kyma.tar.gz
```

### Windows

To install Kyma CLI on Windows, download and unzip the [artifact](https://github.com/kyma-project/cli/releases). Remember to adjust your **PATH** environment variable.

>**NOTE**: To install a different release, change the path to point to the desired version:
  >```
  >curl -Lo kyma.tar.gz https://github.com/kyma-project/cli/releases/download/1.2.0/kyma_Darwin_i386.tar.gz
  >```

## Usage

### Commands

Kyma CLI comes with a set of commands:

|     Command        | Child commands   |  Description  | Example |
|--------------------|----------------|---------------|---------|
| `completion`| None| Generates and displays the bash or zsh completion script. | `kyma completion`|
| `console`| None| Launches Kyma Console in a browser window. | `kyma console` |
| `install`| None| Installs Kyma on a cluster based on the current or specified release. | `kyma install`|
| `provision`| `provision minikube`<br> `provision gardener` <br> `provision gcp`| Provisions a new cluster on a platform of your choice. Currently, this command supports cluster provisioning on GCP, Gardener, and Minikube. | `kyma provision minikube`|
| `test`|`test definitions`<br> `test delete` <br> `test list` <br> `test run` <br> `test status`<br> `test logs`<br> | Runs and manages tests on a provisioned Kyma cluster. Using child commands, you can run tests, view test definitions, list and delete test suites, display test status, and fetch the logs of the tests.| `kyma test run` |
| `uninstall`|None| Uninstalls all Kyma-related resources from a cluster. | `kyma uninstall` |
| `version`|None| Shows the cluster version and the Kyma CLI version.|`kyma version`|

For details on particular commands and options, see [this](https://github.com/kyma-project/cli/tree/master/docs/gen-docs) list.

### Use Kyma CLI

Use the following syntax to run the commands from your terminal:

```
kyma {COMMAND} {FLAGS}
```
where:

* **{COMMAND}** specifies the operation you want to perform.
* **{FLAGS}** specify optional flags. For example, use `-v` or `--verbose` for additional information on performed operations.

Example:

```
kyma install --verbose
```

Further usage examples include:

* Install Kyma with Minikube on Mac:

    ```bash
    kyma provision minikube
    kyma install
    ```

* Install Kyma with Minikube on Windows:

    ```bash
    kyma provision minikube
    # follow instructions to add hosts
    kyma install
    ```

* Install Kyma with Minikube on Windows using HyperV:

    ```bash
    kyma provision minikube --vm-driver hyperv --hypervVirtualSwitch {YOUR_SWITCH_NAME}
    # follow instructions to add hosts
    kyma install
    ```

### Kyma CLI as a kubectl plugin

>**NOTE**: To use Kyma CLI as a kubectl plugin, use Kubernetes version 1.12.0 or higher.

A plugin is a standalone executable file with a name prefixed with `kubectl-` .To use the plugin, perform the following steps:

1. Rename the `kyma` binary to `kubectl-kyma` and place it anywhere in your **{PATH}**:

```bash
sudo mv ./kyma /usr/local/bin/kubectl-kyma
```

2. Run `kubectl plugin list` command to see your plugin on the list of all available plugins.

3. Invoke your plugin as a kubectl command:

```bash
$ kubectl kyma version
Kyma CLI version: v0.6.1
Kyma cluster version: 1.0.0
```

For more information on extending kubectl with plugins, read [Kubernetes documentation](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/).

### Kyma CLI stable binaries

Kyma CLI is used in continuous integration jobs that install or uninstall Kyma or provision clusters. To effectively support this, we publish the stable binaries created from the `stable` tag which corresponds to the latest stable version of Kyma CLI.

To download the binaries, run:

```bash
curl -Lo kyma https://storage.googleapis.com/kyma-cli-stable/kyma-darwin # kyma-linux or kyma.exe
chmod +x kyma
```
