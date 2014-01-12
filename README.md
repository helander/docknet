# docknet: Distribution system for docker containers

A container distribution system for docker containers (based on docker, etcd and pipework)


## Basic principles

Each host has an `etcd` daemon running. This provides access to a shared configuration among the hosts. The configuration consists of two data sets:

1. Containers - for each container to be present in the overall system, a set of properties are defined.

2. Map - the map defines for each container the host it is assigned to.


## Scripts

`docknet` is implemented by a few simple scripts:

* `docknet-etcd` - used for starting the `etcd` daemon on each host. The supplied script is just an example. See `etcd` documentation for more details.

* `docknet-bridge` - used for setting up the `docknet` network on each host. It creates a bridge device (`docknet0`) and then binds the physical network device to the bridge.

* `docknet-scan` - scans the configuration (`containers` and `maps`) and determines which containers should execute on the current host. These containers are then created/started and assigned the IP address as given by the configuration.

## Dependencies

The following software needs to be installed on each host in the `docknet` network. 

* [`docker`](http://www.docker.io)

* [`etcd`](https://github.com/coreos/etcd)

* [`pipework`](https://github.com/jpetazzo/pipework)


## Create configuration

Currently no tool is available for editing the `etcd` key/value pairs. Use [`etcdctl`](https://github.com/coreos/etcdctl) to create and update your configuration.

