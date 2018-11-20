[![CircleCI](https://circleci.com/gh/gpii-ops/terraform-provider-helm.svg?style=svg)](https://circleci.com/gh/gpii-ops/terraform-provider-helm)

**GPII TL;DR** 

This is a fork of
[Terrafrom Helm provider](https://github.com/terraform-providers/terraform-provider-helm).

Creating a new release:
- Create a git tag in form `v1.2.3` and push to this repo
- This will trigger [CircleCI pipeline](https://circleci.com/gh/gpii-ops/terraform-provider-helm)
that will cut a GitHub release and publish built binaries (see [releases](https://github.com/gpii-ops/terraform-provider-helm/releases) tab)

---

Terraform Provider for Helm [![Build Status](https://travis-ci.org/mcuadros/terraform-provider-helm.svg?branch=v0.4.0)](https://travis-ci.org/mcuadros/terraform-provider-helm) [![GitHub release](https://img.shields.io/github/release/terraform-providers/terraform-provider-helm.svg)](https://github.com/terraform-providers/terraform-provider-helm/releases) [![license](https://img.shields.io/github/license/terraform-providers/terraform-provider-helm.svg)]()
===========================

This is a [Helm](https://github.com/kubernetes/helm) provider for [Terraform](https://www.terraform.io/).

The provider manages the installed [Charts](https://github.com/kubernetes/charts) in your Kubernetes cluster, in the same way of Helm does, through Terraform. It will also install Tiller automatically if it is not already present.

Contents
--------

* [Installation](#installation)
* [Example](#example)
* [Documentation](https://www.terraform.io/docs/providers/helm/index.html)
  * [Resource: helm_release](https://www.terraform.io/docs/providers/helm/release.html)
  * [Resource: helm_repository](https://www.terraform.io/docs/providers/helm/repository.html)


Installation
------------

### Requirements

*terraform-provider-helm* is based on [Terraform](https://www.terraform.io), this means that you need


- [Terraform](https://www.terraform.io/downloads.html) >=0.10.0
- [Kubernetes](https://kubernetes.io/) >=1.4

### Installation from binaries (recommended)

The recommended way to install *terraform-provider-helm* is use the binary
distributions from the [Releases](https://github.com/terraform-providers/terraform-provider-helm/releases) page. The packages are available for Linux and macOS.

Download and uncompress the latest release for your OS. This example uses the linux binary.

```sh
> wget https://github.com/terraform-providers/terraform-provider-helm/releases/download/v0.6.0/terraform-provider-helm_v0.6.0_linux_amd64.tar.gz
> tar -xvf terraform-provider-helm*.tar.gz
```

Now copy the binary to the Terraform's plugins folder, if is your first plugin maybe isn't present.

```sh
> mkdir -p ~/.terraform.d/plugins/
> mv terraform-provider-helm*/terraform-provider-helm ~/.terraform.d/plugins/
```

### Installation from sources

If you wish to compile the provider from source code, you'll first need [Go](http://www.golang.org) installed on your machine (version >=1.9 is *required*). You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

Clone repository to: `$GOPATH/src/github.com/terraform-providers/terraform-provider-helm`

```sh
> mkdir -p $GOPATH/src/github.com/terraform-providers
> git clone https://github.com/terraform-providers/terraform-provider-helm.git $GOPATH/src/github.com/terraform-providers/terraform-provider-helm
```

Enter the provider directory and build the provider

```sh
> cd $GOPATH/src/github.com/terraform-providers/terraform-provider-helm
> make build
```

Now copy the compiled binary to the Terraform's plugins folder, if is your first plugin maybe isn't present.

```sh
> mkdir -p ~/.terraform.d/plugins/
> mv terraform-provider-helm ~/.terraform.d/plugins/
```

Example
-------

This is a small example of how to install the mariadb chart on your default
kubernetes cluster, since the provider was initialized, all the configuration
is retrieved from the environment. Please read the [documentation](https://www.terraform.io/docs/providers/helm/index.html) for more
information.

You should have a local configured copy of kubectl.

```hcl
resource "helm_release" "my_database" {
    name      = "my-database"
    chart     = "stable/mariadb"

    set {
        name  = "mariadbUser"
        value = "foo"
    }

    set {
        name = "mariadbPassword"
        value = "qux"
    }

    set_string {
        name = "image.tags"
        value = "registry\\.io/terraform-provider-helm\\,example\\.io/terraform-provider-helm"
    }
}
```

License
-------

Mozilla Public License 2.0, see [LICENSE](LICENSE)

