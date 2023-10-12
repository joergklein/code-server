# Install Docker Compose

Docker Compose is a useful tool for running multi-containers Docker applications. Using Docker Compose, we can configure the application’s services in a YAML file that helps you to create and start all services from the defined configurations. It allows different users to launch, run, communicate and close containers using a just single coordinated command.

Docker Compose works in all environments: production, staging, development, testing, etc. It offers different features that are listed below:

- It allows to create and execute multiple isolated environments on a single host
- It preserves volume data used by your services or when containers are created.
- It can reuse the existing containers which is also an effective feature.
- Using Docker Compose, we can use different environment variables in a configuration file and can customize the composition between different environments.

## Download Docker Compose

Use curl to download the Compose file into the `/usr/bin` directory.

```sh
curl -L "https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
```

Output:

```sh
	% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
																 Dload  Upload   Total   Spent    Left  Speed
	0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  100 42.8M  100 42.8M    0     0  45.1M      0 --:--:-- --:--:-- --:--:-- 58.2M
```

Next, set the correct permissions so that the `docker-compose` command is executable.

```sh
chmod +x /usr/bin/docker-compose
```

### Verify the installation.

```sh
docker-compose --version
```

Output:

```sh
Docker Compose version v2.18.1
```

## Uninstall Docker Compose

Login as User root.

```sh
which docker-compose
```

Output:

```sh
/usr/bin/docker-compose
```

```sh
 rm -rf /usr/bin/docker-compose
 ```
