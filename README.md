# MDH

A Vagrant provisioned VM to run Docker containers in for MacOS.

## Prerequisites

* Vagrant
* VirtualBox
* Ansible

## Usage

```
$ git clone git@github.com:seeruk/mdh.git
$ vagrant up
$ export DOCKER_HOST=tcp://192.168.200.2:2375
```

(Or alternatively, add: `export DOCKER_HOST=tcp://192.168.200.2:2375` to whatever shell rc is relevant to your system)

You can also adjust the RAM and CPU count by modifying the following environment variables:

```
$ export MDH_CPUS=8
$ export MDH_MEMORY=8192
```

The defaults are 4 CPU cores, and 4096 MiB of memory.
