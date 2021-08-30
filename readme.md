# Development environment for remote pair programming
**These directions make many assumptions about the host. They are only for use by the author.**


## Create docker-compose command
```shell
BUILD_DIR=build
mkdir -p ${BUILD_DIR}/bin

DOCKER_COMPOSE=${BUILD_DIR}/bin/docker-compose
curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m) -o ${DOCKER_COMPOSE} && chmod +x ${DOCKER_COMPOSE}
```


## Useful bashrc entries
```shell
export project_root=${HOME}/project_root  # TODO: Update path
export DC="${project_root}/build/bin/docker-compose -f ${project_root}/docker/docker-compose.yml"
alias dc="${DC}"
alias doc='docker'
```


## Setting up docker
[Reference: userns-remap](https://docs.docker.com/engine/security/userns-remap/#enable-userns-remap-on-the-daemon)

### Host setup
```shell
sudo groupadd --gid=100000 taxia-runner
sudo useradd --system --uid=100000 --gid=100000 --shell=/usr/bin/nologin taxia-runner
sudo groupadd --gid=101000 developer
sudo useradd --system --uid=101000 --gid=101000 --shell=/usr/bin/nologin developer
sudo usermod -aG developer $(whoami)  # You will need to logout for this to take effect
```

### Copy `etc` files to correct locations
**NOTE!** This overwrites existing files if they are present
```shell
sudo cp docker/config/host/etc.docker.daemon.json /etc/docker/daemon.json
sudo cp docker/config/host/etc.subuid /etc/subuid
sudo cp docker/config/host/etc.subgid /etc/subgid
```


## `${HOME}/.ssh/config` entries
```config
Host remote_devenv
  User developer
  # HostName <Fill in host name and uncomment this line>
  # IdentityFile <Fill in path to private key and uncomment this line>

Host devenv
  User developer
  HostName localhost
  Port 2222
  # IdentityFile <Fill in path to private key and uncomment this line>
```
