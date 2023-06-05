# Install TeX Live

Before Tex Live can be installed, it makes sense to install a few more packages.

Install perl

```bash
dnf install perl
```

Install libnsl

```bash
dnf install libnsl
```

Install inkscape

```bash
dnf install inkscape
```

If you don't want to bother reading the [full install documentation](https://tug.org/texlive/doc/texlive-en/texlive-en.html#installation) and just want to install everything in TeX Live, on a Unix-like system, a minimal recipe follows.

## Non-interactive default installation on anything but Windows

1. cd /tmp # working directory of your choice
2. wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz # or curl instead of wget
3. zcat < install-tl-unx.tar.gz | tar xf -
4. cd install-tl-*
5. perl ./install-tl --no-interaction # as root or with writable destination
6. Finally, prepend /usr/local/texlive/YYYY/bin/PLATFORM to your PATH,
e.g., /usr/local/texlive/2023/bin/x86_64-linux

### Changing defaults

- The default paper size is a4. If you want the default to be letter, add --paper=letter to the install-tl command.
- By default, everything is installed (7+GB).
- To install a smaller scheme, pass --scheme=scheme to install-tl. For example, --scheme=small corresponds to the [BasicTeX variant of MacTeX](https://tug.org/mactex/morepackages.html).
- To omit installation of the documentation resp. source files, pass --no-doc-install --no-src-install to install-tl.
- To change the main installation directories (rarely needed), add --texdir=/install/dir to the install-tl command. To change the location of the per-user directories (where TEXMFHOME and others will be found), specify --texuserdir=/your/dir.
- To change anything and everything else, omit the --no-interaction. Then you are dropped into an interactive installation menu.

### Pre-install: download, cleanup

You do not need to remove an installation of a previous release, or any system-provided TeX; multiple releases of TL can coexist on the same system without conflict.

A separate page describes [various ways to acquire the software](https://tug.org/texlive/acquire.html). It boils down to either [getting the DVD](https://tug.org/texlive/acquire-dvd.html) from a TeX user group ([ideally by becoming a member](https://tug.org/join.html)), or [downloading in various ways](https://tug.org/texlive/acquire-netinstall.html). Except on Windows, your system must provide a standard Perl installation with the usual core modules. (For Windows, TeX Live comes with its own Perl.)

If you're re-installing after a previous attempt, be sure to completely remove your failed installation. By default, this would be in these two directories (on Unix-like systems):

```bash
rm -rf /usr/local/texlive/2022
rm -rf ~/.texlive2022
```

### Installation of TeX Live

The installer supports text, graphical, and batch interfaces:

- **install-tl -gui text** uses a plain text interface (command line) mode. This is the default on Unix-ish systems, including Macs.
- **install-tl -gui** is the default graphical GUI. At startup it offers very few options, but there is an ‘Advanced’ button for more configurability. This is the default on Windows and on Macs. It requires Tcl/Tk, which is present on pre-Monterey versions of MacOS and is provided for Windows.
- **install-tl --profile=profile** does a batch (unattended) installation. To create such a [profile file](https://tug.org/texlive/doc/install-tl.html#PROFILES), it's easiest to start with the `tlpkg/texlive`.profile file which the installer writes at the end of any successful installation.

For information on all of the installer options, run `install-tl --help`, or see the [install-tl documentation page](https://tug.org/texlive/doc/install-tl.html).


Once you have the TeX Live distribution, run the [install-tl](https://tug.org/texlive/doc/install-tl.html) script to install, like this:

```bash
cd /install-tl-20230520/
perl install-tl -gui text
 <O> options:
	[ ] use letter size instead of A4 by default
	[X] allow execution of restricted list of programs via \write18
	[X] create all format files
	[X] install macro/font doc tree
	[X] install macro/font source tree
	[X] create symlinks to standard directories

 <V> set up for portable installation

Actions:
 <I> start installation to hard disk
 <P> save installation profile to 'texlive.profile' and exit
 <Q> quit

Enter command:
```

To change the installation directories or other options, read the prompts and instructions. The default is to install into parallel directories named by the release year, so that any given release can be run independently, merely by adjusting the search path.

### Choosing a download host

It can take an hour or more to copy all the files, depending on the installation method. If you are downloading over the network, by default a nearby [CTAN mirror](https://ctan.org/mirrors) is automatically chosen. If you have problems, we recommend choosing a specific mirror and then run `install-tl --location http://mirror.example.org/ctan/path/systems/texlive/tlnet` instead of relying on the automatic redirection.

### Post-install: setting PATH

After the installation finishes, you must add the directory of TeX Live binaries to your PATH—except on Windows, where the installer takes care of this. The installer shows the exact lines that should be added. As an example, for Bourne-compatible shells (e.g., in `~/.profile` or `~/.bashrc`):

```bash
PATH=/usr/local/texlive/2023/bin/x86_64-linux:$PATH
```

Use the initialization file and syntax for your shell, your installation directory, and your binary platform name instead of x86_64-linux. After editing the init file, log out and log back in.

If you have multiple TeX installations on a given machine, you need to change the search path to switch between them [except on MacOSX](https://tug.org/mactex/multipletexdistributions.html).

### Post-install: setting the default paper size

The default is to configure the programs for the A4 paper size. To make the default be 8.5 x 11 letter-size paper, you can use the `o` menu option before `i` (nstalling), or run tlmgr paper letter after installation (and after setting your PATH).

### Testing

After a successful installation, please try processing simple test documents, such as latex small2e.

If you're looking for a front-end with which to edit files: TeX Live installs [TeXworks](https://tug.org/texworks) on Windows, and MacTeX installs [TeXShop](https://pages.uoregon.edu/koch/texshop). A [plethora of dedicated TeX editors](https://tug.org/interest.html#editors) are also available. In addition, any plain text editor will work.

### Getting updates

If you want to update packages from CTAN after installation, see these [examples of using tlmgr](https://tug.org/texlive/doc/tlmgr.html#EXAMPLES). This is not required, or even necessarily recommended; it's up to you to decide if it makes sense to get continuing updates in your particular situation.

Typically the main binaries are not updated in TeX Live between major releases. If you want to get updates for LuaTeX and other packages and programs that aren't officially released yet, they may be available in the [TLContrib repository](http://contrib.texlive.info), or you may need to [compile the sources](https://tug.org/texlive/svn) yourself.

### Reporting problems

Please see the [known issues](https://tug.org/texlive/bugs.html) page for bug reporting info. And please [check the documentation](https://tug.org/texlive/doc/texlive-en/texlive-en.html).