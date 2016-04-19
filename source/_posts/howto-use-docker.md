---
title: Docker 入门
tags:
  - howto
  - docker
categories:
  - howto
  - coding
date: 2016-01-13 18:00:45
---


## 简介 ##
我从14年年底开始关注docker容器生态的发展，短短两年见识了Docker的几近“燎原之势”，感慨互联网之迅猛之余，想着也该写篇文章来记录一下我的Docker成长之路。一切都将从那个炎热的中午开始...

## 安装 ##
目前docker的最新版本为1.10.3
linux（ubuntu）
```bash
$ sudo apt-get update && sudo apt-get install curl
$ curl -fsSL https://get.docker.com/gpg | sudo apt-key add -
$ curl -fsSL https://get.docker.com | sh
```

windows
可以通过choco包管理器安装[详情](/howto-use-windows-choco.md)
```cmd
cinst docker -y
cinst docker-machine -y
cinst docker-compose -y
可以通过下载[Docker Toolbox](https://github.com/docker/toolbox/releases/download/v1.10.3/DockerToolbox-1.10.3.exe)安装，Toolbox集成了Docker Engine,docker-machine,docker-compose以及Kitematic Beta版
注：安装前，请先安装依赖的virtualbox。

macos
同windows
mac用户可以通过homebrew管理器安装
```bash
$ brew install docker
$ brew install docker-machine
$ berw install docker-compose
```
或者homebrew cask安装Docker Toolbox
```bash
$brew cask install dockertoolbox
```
或者通过下载[Docker Toolbox](https://github.com/docker/toolbox/releases/download/v1.10.3/DockerToolbox-1.10.3.pkg)安装

## 命令概览 ##
```bash
Usage: docker [OPTIONS] COMMAND [arg...]
       docker daemon [ --help | ... ]
       docker [ --help | -v | --version ]

A self-sufficient runtime for containers.

Options:

  --config=~/.docker              Location of client config files
  -D, --debug                     Enable debug mode
  -H, --host=[]                   Daemon socket(s) to connect to
  -h, --help                      Print usage
  -l, --log-level=info            Set the logging level
  --tls                           Use TLS; implied by --tlsverify
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file
  --tlskey=~/.docker/key.pem      Path to TLS key file
  --tlsverify                     Use TLS and verify the remote
  -v, --version                   Print version information and quit

Commands:
    attach    Attach to a running container
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    cp        Copy files/folders between a container and the local filesystem
    create    Create a new container
    diff      Inspect changes on a container's filesystem
    events    Get real time events from the server
    exec      Run a command in a running container
    export    Export a container's filesystem as a tar archive
    history   Show the history of an image
    images    List images
    import    Import the contents from a tarball to create a filesystem image
    info      Display system-wide information
    inspect   Return low-level information on a container or image
    kill      Kill a running container
    load      Load an image from a tar archive or STDIN
    login     Register or log in to a Docker registry
    logout    Log out from a Docker registry
    logs      Fetch the logs of a container
    network   Manage Docker networks
    pause     Pause all processes within a container
    port      List port mappings or a specific mapping for the CONTAINER
    ps        List containers
    pull      Pull an image or a repository from a registry
    push      Push an image or a repository to a registry
    rename    Rename a container
    restart   Restart a container
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    save      Save an image(s) to a tar archive
    search    Search the Docker Hub for images
    start     Start one or more stopped containers
    stats     Display a live stream of container(s) resource usage statistics
    stop      Stop a running container
    tag       Tag an image into a repository
    top       Display the running processes of a container
    unpause   Unpause all processes within a container
    update    Update resources of one or more containers
    version   Show the Docker version information
    volume    Manage Docker volumes
    wait      Block until a container stops, then print its exit code

Run 'docker COMMAND --help' for more information on a command.

```

## 常用命令 ##
搜索镜像
docker search image_name
列出本地镜像
docker images
拉取镜像
docker pull [(url:port/)image_name(:tag)]
构建镜像
docker build [Dockerfile目录]
运行镜像
docker run -d image_name
docker run -ti image_name /bin/bash
停止容器
docker stop contain_name
删除容器
docker rm [contain_name]
删除镜像
docker rmi image_name
给镜像打tag
docker tag contain_name tagname

## docker machine ##
### 命令概览 ###
```bash
Usage: docker-machine.exe [OPTIONS] COMMAND [arg...]

Create and manage machines running Docker.

Version: 0.6.0, build e27fb87

Author:
  Docker Machine Contributors - <https://github.com/docker/machine>

Options:
  --debug, -D						Enable debug mode
  -s, --storage-path "C:\Users\Admin\.docker\machine"	Configures storage path [$MACHINE_STORAGE_PATH]
  --tls-ca-cert 					CA to verify remotes against [$MACHINE_TLS_CA_CERT]
  --tls-ca-key 						Private key to generate certificates [$MACHINE_TLS_CA_KEY]
  --tls-client-cert 					Client cert to use for TLS [$MACHINE_TLS_CLIENT_CERT]
  --tls-client-key 					Private key used in client TLS auth [$MACHINE_TLS_CLIENT_KEY]
  --github-api-token 					Token to use for requests to the Github API [$MACHINE_GITHUB_API_TOKEN]
  --native-ssh						Use the native (Go-based) SSH implementation. [$MACHINE_NATIVE_SSH]
  --bugsnag-api-token 					BugSnag API token for crash reporting [$MACHINE_BUGSNAG_API_TOKEN]
  --help, -h						show help
  --version, -v						print the version
  
Commands:
  active		Print which machine is active
  config		Print the connection config for machine
  create		Create a machine
  env			Display the commands to set up the environment for the Docker client
  inspect		Inspect information about a machine
  ip			Get the IP address of a machine
  kill			Kill a machine
  ls			List machines
  provision		Re-provision existing machines
  regenerate-certs	Regenerate TLS Certificates for a machine
  restart		Restart a machine
  rm			Remove a machine
  ssh			Log into or run a command on a machine with SSH.
  scp			Copy files between machines
  start			Start a machine
  status		Get the status of a machine
  stop			Stop a machine
  upgrade		Upgrade a machine to the latest version of Docker
  url			Get the URL of a machine
  version		Show the Docker Machine version or a machine docker version
  help			Shows a list of commands or help for one command
  
Run 'docker-machine.exe COMMAND --help' for more information on a command.

```

## docker compose ##
### 命令概览 ###

```bash
Define and run multi-container applications with Docker.

Usage:
  docker-compose [-f=<arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE           Specify an alternate compose file (default: docker-compose.yml)
  -p, --project-name NAME   Specify an alternate project name (default: directory name)
  --verbose                 Show more output
  -v, --version             Print version and exit

Commands:
  build              Build or rebuild services
  config             Validate and view the compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  events             Receive real time events from containers
  help               Get help on a command
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pulls service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information
```

### YML文件 ###
