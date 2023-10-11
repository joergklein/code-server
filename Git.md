# Install Git

Install Git using the dnf command:

```sh
dnf install git
```

## Git Setup
Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once on any given computer; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

- **[path]/etc/gitconfig file**: Contains values applied to every user on the system and all their repositories. If you pass the option `--system` to `git config`, it reads and writes from this file specifically. Because this is a system configuration file, you would need administrative or superuser privilege to make changes to it.

- **~/.gitconfig or ~/.config/git/config file**: Values specific personally to you, the user. You can make Git read and write to this file specifically by passing the `--global` option, and this affects all of the repositories you work with on your system.

- **config** file in the Git directory (that is, `.git/config`) of whatever repository you’re currently using: Specific to that single repository. You can force Git to read from and write to this file with the `--local` option, but that is in fact the default. Unsurprisingly, you need to be located somewhere in a Git repository for this option to work properly.

### Your Identity

The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

```sh
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

### Your Editor
Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message. If not configured, Git uses your system’s default editor.

If you want to use a different text editor, such as Emacs, you can do the following:

```sh
git config --global core.editor vim
```

### Your default branch name

By default Git will create a branch called master when you create a new repository with `git init`. From Git version 2.28 onwards, you can set a different name for the initial branch.

To set main as the default branch name do:

```sh
git config --global init.defaultBranch main
```

### Checking Your Settings
If you want to check your configuration settings, you can use the `git config --list` command to list all the settings Git can find at that point:

```sh
git config --list
```

Output:

```sh
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
```

You may see keys more than once, because Git reads the same key from different files (`[path]/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

You can also check what Git thinks a specific key’s value is by typing `git config <key>`:

```sh
git config user.name
```

Output:

```sh
John Doe
```