# Install Ansible

Ansible is a free and open source automation tool that allows system administrators to configure and control hundreds of nodes from a centralized server without requiring installed agents. It uses the SSH protocol to communicate with remote nodes. Ansible is the preferred management solution over Puppet and Chef because of its ease of use and installation.

Ansible can be used in provisioning to build up the numerous servers required in your architecture. Ansible is a tool for configuration management that may be used to start and stop services, install or update software, implement security policies, and carry out a broad range of other configuration-related operations. Ansible makes DevOps easier by enabling the automatic deployment of internally developed applications to your production systems.

## Update the System

It is essential to ensure your existing operating version is up-to-date before installing new software. Update your system by executing the below command.

```bash
sudo dnf update
```

### Configure the EPEL Repository

The Ansible package and its dependencies are unavailable in AlmaLinux 9's default package repositories. The EPEL repository must first be configured to install Ansible AlmaLinux using the dnf command.

Install the EPEL repository on the system by executing the below command.

```bash
sudo dnf install epel-release
```

## Install Ansible with the dnf command
Execute the below command to install the Ansible package from the EPEL repository.

```bash
sudo dnf install ansible
```

After successfully installing Ansible and its dependencies, verify its version by executing the below command.

```bash
ansible --version
```

Output:

```bash
ansible [core 2.13.3]
config file = /etc/ansible/ansible.cfg
configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/lib/python3.9/site-packages/ansible
ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
executable location = /usr/bin/ansible
python version = 3.9.14 (main, Jan  9 2023, 00:00:00) [GCC 11.3.1 20220421 (Red Hat 11.3.1-2)]
jinja version = 3.1.2
libyaml = True
```

## Install Ansible with Pip

If you wish to install the most recent version of Ansible, you can use Pip. To install Ansible on AlmaLinux with Pip, follow the below steps.

### Install All Updates

Update your system by executing the below command.

```bash
sudo dnf update
```

### Install Python and Other Dependencies

Execute the below command to install Pip with Python 3.9 and other dependencies.

```bash
sudo dnf  install python3-pip
sudo pip3 install --upgrade pip
```

Verify that you've installed Python and Pip by opening a command prompt and typing the following command:

```bash
python -V
```

Output:

```bash
Python 3.9.13
```

```bash
pip3 --version
```

Output:

```bash
pip 23.0.1 from /usr/local/lib/python3.9/site-packages/pip (python 3.9)
```

### Install the Latest Version of Ansible With Pip

Execute the below commands one by one to install Ansible with Pip.

```bash
sudo pip3 install setuptools-rust wheel
sudo python -m pip install ansible
```

After successfully installing Ansible, verify its version by executing the below command.

```bash
ansible --version
```

Output:

```bash
ansible [core 2.14.3]
config file = None
configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/local/lib/python3.9/site-packages/ansible
ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
executable location = /usr/local/bin/ansible
python version = 3.9.14 (main, Jan  9 2023, 00:00:00) [GCC 11.3.1 20220421 (Red Hat 11.3.1-2)] (/bin/python)
jinja version = 3.1.2
libyaml = True
```

### Verify the Ansible Installation

Ansible's default configuration file, `ansible.cfg`, is automatically created under the `/etc/ansible` folder when installed using the dnf or yum commands.

> If you install Ansible via Pip, you must manually build its configuration file. It is recommended that ansible.cfg files be created for each project.

The following commands create a project called `project-ansible` for the demonstration.

```bash
cd /etc
mkdir project-ansible
cd project-ansible
```

Create the `ansible.cfg` file under the folder `project-ansible` with the following details and save the file.

```bash
[defaults]
inventory = /home/ansible-admin/project-ansible/inventory
remote_user = ansible-admin
host_key_checking = False

[privilege_escalation]
become=True
become_method=sudo
become_user=root
become_ask_pass=False
```

Then, create an `inventory` file under the folder `project-ansible`` with the following details and save the file.

```bash
[Hostserver1]
172.31.2.186

[Hostserver2]
172.31.2.187
```

Now, you must create SSH keys for your remote_user and share them among all the managed host servers. Here, `ansible-admin` is a remote_user.

```bash
ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ansible-admin/.ssh/id_rsa):
Created directory '/home/ansible-admin/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ansible-admin/.ssh/id_rsa.
Your public key has been saved in /home/ansible-admin/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:MYbYFfbWGwV3SuyhDShArL+4MD9hVng1OzR6UgHzqOE ansible-admin@ansible-node
The key's randomart image is:
+---[RSA 3072]----+
|     o=o=o ..o+ .|
|     o.BB....+oo |
|    oo+===o o=.. |
|   .oo=.++  .oo  |
|    E+ oS.  .    |
|    + .          |
|  oo o .         |
|   +o .          |
|    oo           |
+----[SHA256]-----+
```

You can now share the SSH keys using the ssh-copy-id command.

```bash
$ ssh-copy-id ansible-admin@172.31.2.186
$ ssh-copy-id ansible-admin@172.31.2.187
```

Output:

```bash
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansible-admin/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansible@172.31.2.186's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible-admin@172.31.2.186'"
and check to make sure that only the key(s) you wanted were added.

[ansible-admin@ansible-node ~]$ ssh-copy-id ansible-admin@172.31.2.187
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansible-admin/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansible@172.31.2.187's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible-admin@172.31.2.187'"
and check to make sure that only the key(s) you wanted were added.
```

Execute the below command on each managed host server to run all the commands without prompting a password.

```bash
echo "ansible-admin ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible-admin
```

Using the ping module, verify the connectivity from the control node to managed hosts.

```bash
ansible -i inventory all -m ping
```

Output:

```bash
172.31.2.186 | SUCCESS => {
	"ansible_facts": {
			"discovered_interpreter_python": "/usr/libexec/platform-python"
	},
	"changed": false,
	"ping": "pong"
}
172.31.2.187 | SUCCESS => {
	"ansible_facts": {
			"discovered_interpreter_python": "/usr/bin/python3"
	},
	"changed": false,
	"ping": "pong"
}
```

Create a sample playbook

Create a `web.yaml` file under the folder `project-ansible` with the following details and save the file.

```yaml
- name: Play to Packages
	hosts:
		- Hostserver1
		- Hostserver2
	tasks:
	- name: Install php and nginx
		package:
			name:
				- php
				- nginx
			state: present
```

 Run the playbook

```bash
ansible-playbook -i inventory web.yaml
```

Output:

```bash
PLAY [Play to Packages] ********************************************************************

TASK [Gathering Facts] ********************************************************************
ok: [172.31.2.186]
ok: [172.31.2.187]

TASK [Install php and nginx] **************************************************************
changed: [172.31.2.186]
changed: [172.31.2.187]

PLAY RECAP ********************************************************************************
172.31.2.186            : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
172.31.2.187            : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```