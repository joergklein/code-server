## How to configure an SSH key in GitLab

GitLab is a powerful tool for version control and project management, used by developers around the world. When interacting with GitLab, you need to authenticate yourself to ensure that you have access to the projects you’re working on. There are several ways to authenticate with GitLab, including using your username and password or a personal access token.

However, one of the most secure and convenient ways to authenticate with GitLab is by using an SSH key. SSH keys use public key cryptography to authenticate with GitLab, providing a more secure method of authentication than passwords. By adding an SSH key to GitLab, you can avoid exposing your password to potential attackers and enjoy convenient access to GitLab without having to enter your credentials each time.
The first thing you’ll need is your public ED25519  SSH key in text form, to get this, you can use this command it Git Bash:

### Create an SSH key using the following command ssh-keygen

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

For ED25519

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Replace `your_email@example.com` with your email address which you use in GitLab.

When prompted for a filename and a passphrase, you can leave the defaults by pressing enter.

That’s it, when you run the command `ls -al ~/.ssh` you will now see the two files we pointed out above, that’s `id_rsa` and `id_rsa.pub`.

```sh
cat ~/.ssh/id_ed25519.pub | clip
```

Or if you’re using RSA:

```sh
cat ~/.ssh/id_rsa.pub | clip
```

Which will copy the SSH key in text form to your clipboard.

While logged into your GitLab account on `https://gitlab.com`, follow these steps:

1. Select your avatar and click on settings
2. Click SSH Keys
3. Paste the SSH key into the Key field
4. Add a descriptive text in the title as a user or the computer it is used from
5. Click Add Key

### Verify that your SSH key was added correctly.

The following commands use the example hostname `gitlab.example.com`. Replace this example hostname with your GitLab instance’s hostname, for example, `git@gitlab.com`.

```sh
[code-server@localhost .ssh]$ ssh -T git@gitlab.com
```

Output:

```sh
Welcome to GitLab, @your accout!
```
