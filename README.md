# kitchen-docker-vm

OSX w/ kitchen-docker + an ubuntu vm = <3 faster tests <3

This Vagrantfile launches an ephemeral VirtualBox vm that exposes a [Docker](http://www.docker.io/) api capable of running Chef test-kitchen kitchens directly from OSX via [kitchen-docker](https://github.com/portertech/kitchen-docker).

## Prereqs

* [VirtualBox](https://github.com/berkshelf/vagrant-berkshelf)
* [Vagrant](http://www.vagrantup.com/)
* [vagrant-omnibus](https://github.com/schisamo/vagrant-omnibus)
* [vagrant-berkshelf](https://github.com/berkshelf/vagrant-berkshelf)
* [Docker CLI](http://davekonopka.share.s3.amazonaws.com/chef/docker) installed on OSX

### Installing the Docker client on OSX

[Pull down a binary](http://davekonopka.share.s3.amazonaws.com/chef/docker) or build your own on OSX with Go. Either way the Docker CLI needs to be in your path on the OSX side. 

* The Docker versions **must match** between host & guest or this will not work.
* kitchen-docker expects Docker v0.6.6 at this point. Using an earlier version breaks kitchen operations.
* The Docker daemon does not run on OSX. The CLI is used for communication.

## Usage

```
bundle install
vagrant up
```

### Example .kitchen.yml

```
---
driver_plugin: docker
driver_config:
  use_sudo: false
  socket: tcp://192.168.101.101:4242
  require_chef_omnibus: :latest

platforms:
- name: ubuntu-12.04
  driver_config:
    image: ubuntu:12.04
    platform: ubuntu
- name: centos-6.4
  driver_config:
    image: centos:6.4
    platform: centos
```

`kitchen create` <-- Magic.

## Credit

This repo is heavily inspired by [@portertech](https://twitter.com/portertech)'s [efforts](https://github.com/portertech/lxc-vm).