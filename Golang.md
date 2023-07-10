# Install Golang

For other content on installing, you might be interested in:

- [Managing Go installations](https://go.dev/doc/manage-install) -- How to install multiple versions and uninstall.
- [Installing Go from source](https://go.dev/doc/install/source) -- How to check out the sources, build them on your own machine, and run them.

Don't see your operating system here? Try one of the other [downloads](https://go.dev/dl/).

1. Remove any previous Go installation by deleting the `/usr/local/go` folder (if it exists), then extract the archive you just downloaded into `/usr/local`, creating a fresh Go tree in `/usr/local/go`:

```bash
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.4.linux-amd64.tar.gz
```

**Do not** untar the archive into an existing `/usr/local/go` tree. This is known to produce broken Go installations.

1. Add `/usr/local/go/bin` to the PATH environment variable.

You can do this by adding the following line to your `$HOME/.profile` or `/etc/profile` (for a system-wide installation):

```bash
export PATH=$PATH:/usr/local/go/bin
```

> VS Code need an additional entry in `/etc/bashrc`


**Note**: Changes made to a profile file may not apply until the next time you log into your computer. To apply the changes immediately, just run the shell commands directly or execute them from the profile using a command such as source `$HOME/.profile`.

3. Verify that you've installed Go by opening a command prompt and typing the following command:

```bash
go version
````

Output:

```bash
go version go1.20.4 linux/amd64
```

Confirm that the command prints the installed version of Go.