# Setup SSH Passwordless Login

**Secure Shell**, popularly known as **SSH**, is a secure network protocol that allows users to securely connect to remote hosts such as servers. It is based on a client-server architecture and uses two main authentication methods – **password** and **ssh-key** pair authentication.

The **SSH-key** pair authentication employs the use of SSH keys which are cryptographic keys used to authenticate and secure communication between the client and the server. SSH-key pair authentication is preferred over password authentication as it provides safer authentication which is not susceptible to brute-force attacks.

## Creating RSA SSH Key Pair

To start the show, we will create an **RSA** key pair which comprises a public and private key. We will demystify these keys later on in the guide. To create the key pair, run the command:

```bash
ssh-keygen
OR
ssh-keygen -t rsa
```

The above commands create a **2048**-bit RSA key pair which is considered good enough to offer decent encryption to secure communication. However, you can create a **4096**-bit key pair that is more robust and offers better encryption.

To do this, simply pass the `-b` flag. This is exactly what we are going to do.

```bash
ssh-keygen -b 4096
```

Output:

```bash
Generating public/private rsa key pair.
```

Right after you press **ENTER**, you will be asked to provide the path in which the keys will be stored. By default, this is the **~/.ssh** directory. Unless required to change it to a different path, just go with the default directory by pressing **ENTER**.

Output:

```bash
Enter file in which to save the key (/root/.ssh/id_rsa):
```

Thereafter, you will be required to provide a passphrase or a password. While optional, this adds an extra layer of protection when authenticating.

However, this is limiting when you want to configure passwordless ssh-key authentication to a remote host. If this is your goal, then simply press **ENTER** to skip providing the keyphrase.

Output:

```bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

Output:

```bash
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:xM+5Yslv1O81srU0d7GSXLKAkW/lnfpJTcMdnd/RzOE root@localhost
The key's randomart image is:
+---[RSA 4096]----+
|               . |
|       .  .   .o=|
|        oo   . E=|
|       . o+.o o B|
|        S.+= o B=|
|       . .o.+ *.=|
|        =..  O B=|
|       . o.   X.B|
|         ..  o.+ |
+----[SHA256]-----+
```

At this point, your keys should be stored in the *~/.ssh* directory which is a hidden directory in your home directory. Just to confirm this, run the command:

```bash
ls -la ~/.ssh
```

Output:

```bash
total 20
drwx------  2 root root  103 May 30 08:54 .
dr-xr-x---. 7 root root 4096 May 23 11:17 ..
-rw-------  1 root root    0 May 21 13:48 authorized_keys
-rw-------  1 root root 3381 May 30 08:54 id_rsa
-rw-r--r--  1 root root  740 May 30 08:54 id_rsa.pub
-rw-------  1 root root  274 May 21 14:56 known_hosts
-rw-r--r--  1 root root   97 May 21 14:56 known_hosts.old
```

A few points to note:

- The **id_rsa** is the private key. As the name suggests this should be kept extremely confidential and should never be divulged or shared. An attacker can easily compromise your remote host once they get a hold of the private key.
- The **id_rsa.pub** is the public key, which can be shared without any problem. You can save it to any remote host that you want to connect to.

## Copy SSH Public Key to Remote Linux Server

The next step is to copy or transfer the public key to the remote server or host. You can do this manually, but the ssh-copy-id command easily allows you to do this.

The **ssh-copy-id** command takes the following syntax:

```bash
ssh-copy-id user@remote-host-ip-address
```

In our setup, we have a remote host with IP **172.103.125.146** and a configured remote user called **joerg**.

To copy the public SSH key, we will run the command:

```bash
ssh-copy-id joerg@172.103.125.146
```

If this is the first time connecting to the host, you will get the output shown below. To proceed with the authentication, type **yes** and hit **ENTER** to proceed.

On your local system, the **known_hosts** file is created in the **~/.ssh** directory. The file contains the SSH fingerprints for remote hosts that you have connected to.

```bash
-rw-------  1 root root 3381 May 30 08:54 id_rsa
-rw-r--r--  1 root root  740 May 30 08:54 id_rsa.pub
-rw-------  1 root root  274 May 21 14:56 known_hosts
```

You can view it as follows.

```bash
cat ~/.ssh/known_hosts
```

Output:

```bash
217.160.197.142 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINbBMvvDjN4IP04VAZlDH42A+HL25ifeIK9CorAvaMA/
217.160.197.142 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFjDE2sDVlaHhXudMMsLEuJvY+nBuTbwLGpQkLaJ5oxIR9vXinw/2dSzqnDAlrmJ1ZgWKQnvPh7Mz770Hp/sobU=
```

## SSH Passwordless Login to Remote Linux

With the public key now saved on the remote host, we can now login to the remote host without SSH password authentication. To test this, we will try logging in normally to the remote host.

```bash
ssh joerg@172.103.125.146
```

From the output, you can see that we straight away dropped to the remote system’s shell. This confirms that we have successfully configured **SSH** Passwordless authentication.

Now confirm that the public key is saved in the **authorized_keys** file on the remote host.

```bash
ls -la ~/.ssh/
```

Output:


```bash
-rw-------  1 joerg joerg 3381 May 30 08:54 .
-rw-r--r--  1 joerg joerg  740 May 30 08:54 ..
-rw-------  1 joerg joerg  274 May 21 14:56 authorized_keys
```

To view the file, use the `cat command` as follows:

```bash
cat ~/.ssh/authorized_keys
```

## Disable SSH Password Authentication

We are not yet done, the password authentication is still enabled and this can potentially subject the remote server or host to brute-force attacks.

To eliminate this attack vector, it is highly advised to disable password authentication. This ensures that login is only possible through an SSH key pair. To achieve this, open the **sshd_config** file which is the main SSH configuration file.

```bash
sudo vim /etc/ssh/sshd_config
```

Locate the PasswordAuthentication directive. If commented out, uncomment it and set it to `no`.

Save the changes and exit the file. Then restart SSH to apply the change made.

```bash
sudo systemctl restart sshd
```

This successfully disables password authentication and only users with the private SSH key can log in.

At this point, SSH password authentication has been disabled on the remote server and the only possible way of accessing the remote server is through **public-key** authentication.
