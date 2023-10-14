# Install R

**R** is a programming language as well as a software environment for graphical representation of data and statistical computing supported by the **R** Foundation. This integrated suite can be used for data calculation, manipulation, and graphical display.

It has the following components:

- An effective data handling and storage facility
- A set of operators for calculations on arrays, in particular, matrices
- Graphical facilities for data analysis and display either on-screen or on hardcopy.
- A large, coherent, integrated collection of intermediate tools for data analysis

**R** was developed by Ross Ihaka and Robert Gentleman at the University of Auckland. The name **R** was derived from the first letter of the two **R** authors. Currently, it is widely used by developers to develop statistical and data analysis software. It is referred to as an environment rather than a programming language to characterize it as a fully planned and coherent system. It offers an environment within which statistical techniques are implemented. **R** can also be extended through packages provided by the **R** distribution and via the CRAN family.

The file types associated with **R** include:

- ***.rmd**: R Markdown file
- ***.r**: R script
- ***.rnw**: R Sweave file
- ***.rds**: A file containing a single R object. It can be created using saveRDS() and loaded with readRDS()
*.rdata: contains one or more R objects/workspaces. It can be created using save() and loaded with load().

Full-time `R developers`, required an integrated development environment(IDE). The `RStudio` acts as the integrated development environment for **R**.

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

**R** is a meta-package that contains all the required **R** components.

Verify the installation by printing the **R** version:

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

##  Getting Started With R

Once installed, R can be used from the console. To launch the R console, execute the command:

```sh
R
```

### Install the additional packages in R

```sh
install.packages("languageserver")
```

#### The following software or extensions are recommended to enhance the experience of using R in VS Code:

- [radian](https://github.com/randy3k/radian): is an alternative console for the **R** program with multiline editing and rich syntax highlight. One would consider _radian_ as a [ipython](https://github.com/ipython/ipython) clone for **R**, though its design is more aligned to [julia](https://julialang.org).
- [VS Code-R-Debugger](https://github.com/ManuelHentschel/VSCode-R-Debugger): this extension adds debugging capabilities for the [R](https://www.r-project.org/) programming language to Visual Studio Code and depends on the **R** package [vscDebugger](https://github.com/ManuelHentschel/vscDebugger) ([documentation](https://manuelhentschel.github.io/vscDebugger/)). For further **R** support in VS Code see [vscode-R](https://github.com/Ikuyadeu/vscode-R).
- [httpgd](https://github.com/nx10/httpgd): a graphics device for **R** that is accessible via network protocols. This package was created to make it easier to embed live **R** graphics in integrated development environments and other applications. The included HTML/JavaScript client (plot viewer) aims to provide a better overall user experience when dealing with R graphics. The device asynchronously serves graphics via HTTP and WebSockets.
