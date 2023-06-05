# Install Docker

We have covered the installation steps for setting up Docker packages on Almalinux using the command terminal in this tutorial.

## Add Docker Repository

Just like the previous version of Almalinux 8, the 9 also not offers Docker’s latest packages to install. So, we manually run the given command to enable the Docker repository on Almalinux 9.

```bash
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

## Docker installation

Once the system is ready, we can execute the main installation command to configure Docker CE on Almalinux 9. This will install the dependencies and extra packages we required to run this open-source container service on RHEL-based Linux systems.

```bash
sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Start Docker Service

Next, we start and enable the Docker service and after that, we will go through a command that will let’s know whether it is working fine without any errors or not.

```bash
sudo systemctl enable --now docker
```

To check the service status:

```bash
sudo systemctl status docker
```

Output:

```bash
systemctl status docker
● docker.service - Docker Application Container Engine
	  Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
	  Active: active (running) since Sun 2023-05-21 13:56:26 UTC; 19h ago
TriggeredBy: ● docker.socket
		 Docs: https://docs.docker.com
	Main PID: 13344 (dockerd)
		Tasks: 101
	  Memory: 587.8M
		  CPU: 1min 22.835s
	  CGroup: /system.slice/docker.service
				 ├─13344 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
				 ├─13749 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 9000 -container-ip 172.17.0.2 -container-port 9000
				 ├─13758 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 9000 -container-ip 172.17.0.2 -container-port 9000
				 ├─13771 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 8000 -container-ip 172.17.0.2 -container-port 8000
				 ├─13779 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 8000 -container-ip 172.17.0.2 -container-port 8000
				 ├─16283 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 443 -container-ip 172.18.0.3 -container-port 443
				 ├─16292 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 443 -container-ip 172.18.0.3 -container-port 443
				 ├─16308 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 81 -container-ip 172.18.0.3 -container-port 81
				 ├─16316 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 81 -container-ip 172.18.0.3 -container-port 81
				 ├─16331 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 80 -container-ip 172.18.0.3 -container-port 80
				 └─16337 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 80 -container-ip 172.18.0.3 -container-port 80
```

### Add non-root user to Docker group

By default to run the Docker command, we need to use the sudo every time with it. To remove it, we can add our current user to the Docker group. After that, we can run the Docker command tool to create containers without the sudo rights.

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Test Docker using Hello-World Image

We have already completed all the steps required to set up and configure the Docker on AlmaLinux 9. Now, let’s test our Docker command line to confirm it is working and creating containers without producing any common errors.

```bash
docker run hello-world
```

If the output of the above command contains this text:

```bash
Hello from Docker! This message shows that your installation appears to be working correctly.
```

Then your installation is correct and you want to create docker containers.

## Uninstall Docker

Later after completing your testing or project, if you don’t require the container service then you can remove the Docker any time by running the given commands:

```bash
sudo dnf remove -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
