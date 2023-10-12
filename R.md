# Install R

**R** is a fast growing open source programming language that specializes in statistical computing and graphical representation.

## System requirements

- Minimum 1 GB RAM

## Prepare Your System

Before we begin, there are a number of packages required. Begin by updating the available system packages:

```sh
dnf update
```

The **R** packages are not included in the AlmaLinux core repository. We will install **R** from the **EPEL** repository.


Enable the EPEL and POwerTools(CRB) on AlmaLinux.

```sh
dnf install epel-release
dnf config-manager --set-enabled crb
```

## Install R for the command line

**R** can now be installed from AlmaLinux

```sh
dnf install R
```

**R** is a meta-package that contains all the required R components.

Verify the installation by printing the R version:

```sh
R --version
```

Output:

```sh
R version 4.3.0 (2023-04-21) -- "Already Tomorrow"
Copyright (C) 2023 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```
