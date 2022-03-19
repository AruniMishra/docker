# Content

- [Content](#content)
  - [Installation](#installation)
    - [Windows](#windows)
  - [Window Terminal using WSL](#window-terminal-using-wsl)
    - [Uninstall old versions](#uninstall-old-versions)
      - [Set up the repository](#set-up-the-repository)
      - [Install Docker Engine](#install-docker-engine)
  - [Start service](#start-service)
  - [Command to run](#command-to-run)
  - [MySQL](#mysql)

## Installation

### [Windows](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

- install WSL

  - Enable the Windows Subsystem for Linux

    ```console
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```

  - Enable Virtual Machine feature

    ```console
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```

  - Set WSL 2 as your default version

    ```console
    wsl --set-default-version 2
    ```

## [Window Terminal using WSL](https://docs.docker.com/engine/install/ubuntu/)

### Uninstall old versions

Older versions of Docker were called `docker`, `docker.io`, or `docker-engine`.
If these are installed, uninstall them:

```console
sudo apt-get remove docker docker-engine docker.io containerd runc
```

#### Set up the repository

1. Update the `apt` package index and install packages to allow `apt` to use a
   repository over HTTPS:

   ```console
   $ sudo apt-get update

   $ sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg \
       lsb-release
   ```

2. Add Docker's official GPG key:

   ```console
   curl -fsSL {{ download-url-base }}/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

3. Use the following command to set up the **stable** repository.

   ```console
   $ echo \
     "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] {{ download-url-base }} \
     $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

#### Install Docker Engine

1. Update the `apt` package index, and install the _latest version_ of Docker
    Engine and containerd, or go to the next step to install a specific version:

    ```console
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```

2. To install a _specific version_ of Docker Engine, list the available version

    a. List the versions available in your repo:

    ```console
    apt-cache madison docker-ce
    ```

    b. Install a specific version using the version string from the second column,
    for example, `5:18.09.1~3-0~ubuntu-xenial`.

   ```bash
   sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
   ```

3. Verify that Docker Engine is installed correctly by running the `hello-world`
    image.

    ```console
    sudo docker run hello-world
    ```

## Start service

```console
service --status-all
sudo service docker start
```

---

## Command to run

```console
docker run -d -p 80:80 docker/getting-started
```

```console
docker stop $(docker ps -aq)
```

- Nginx

```bash
docker run --name some-nginx -p 80:80 -d nginx
```

---

To delete all containers including its volumes use

```console
docker rm -vf $(docker ps -a -q)
```

To delete all the images,

- view image:

    ```console
    docker image ls
    ```

    Or,

    ```console
    docker images -a
    ```

```console
docker rmi -f $(docker images -a -q)
```

add to uermod

```console
sudo usermod -aG docker aruni
```

On Linux, you can also run the following command to activate the changes to groups:

```console
 newgrp docker 
```

## MySQL

1. run my sql

   e: env variable

   ```console
   docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
   ```

   Or,

   ```console
   docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -dp 3306:3306 --rm mysql
   ```

1. find ip adress

   ```console
   docker inspect containerId --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
   ```

1. connect to mysql

   Install mysql(client) if not installed - Ubuntu

   ```console
   sudo apt-get install mysql-client
   ```

   ```console
   sudo mysql -h 172.17.0.2 -P 3306 --protocol=tcp -u root -p
   ```

   Or (If post mapping specified during docker run)

   ```console
   sudo mysql -h 127.0.0.1 -P 3306 -u root -p
   ```

   Or,

   ```console
   docker exec -it some-mysql mysql -uroot -p
   ```
