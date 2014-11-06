OSXContainerHost
================

A Vagrant provisioned VM to run Docker containers in.

## Prerequisites

* Vagrant
* VirtualBox
* Ansible

## Usage

```
$ git clone git@github.com:SeerUK/OSXContainerHost.git
$ vagrant up
$ export DOCKER_HOST=tcp://192.168.200.2:2375
```

(Or alternatively, add: `export DOCKER_HOST=tcp://192.168.200.2:2375` to whatever shell rc is relevent to your system)

## Things to be wary of

* NFS is configured to map all activity in `/Users/` to the uid and gid you run Vagrant as. This will also affect volumes in containers if they are mounted from the `/Users/` folder (which I imagine most will be...). Realistically, for most use-cases this shouldn't be a problem, but it is something to be aware of. Please suggest a better solution if there is one.
* Docker containers are created inside the VM, the images are downloaded inside the VM. Everything happens in there; therefore, if you remove and recreate the VM you will lose all of your existing containers.
