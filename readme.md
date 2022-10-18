# Docker

This vagrant will create virtual machine running docker server. The default IP Address is `192.168.2.105` see details in `Vagrantfile`.

## Ingredient

- [Vagrant](https://www.vagrantup.com/downloads)
- Docker Client

> Note: Docker Client can be installed using [Chocolatey](https://community.chocolatey.org/packages/docker) or [Scoop](https://scoop.sh/#/apps?q=docker&s=0&d=1&o=true)

## How to run

Execute `vagrant up` to start the virtual machines. First time start will setup Docker.

Test with Docker Client:

```console
set DOCKER_HOST=192.168.2.105
docker version
```
