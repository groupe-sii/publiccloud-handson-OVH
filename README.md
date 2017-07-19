This container is based on Ubuntu image with both OpenStack client tools and SSH server installed.

# Deploy the container

## Prerequisites

* Having docker installed on your system
* Having a valid OpenStack project access
* Download the `openrc.sh` file (from API access in Horizon GUI)

## Build

## Without SSH server

If not already available in your `docker images`, build the image:

```
$ docker build -t openstack-tools openstack-tools/
```

## With SSH server

Build the `openstack-tools` as described in previous section, then :

```
$ docker build -t openstack-tools-with-ssh openstack-tools-with-ssh/
```

# Run

## Without SSH server

```
$ docker run -ti --rm -v $(pwd)/openrc.sh:/root/openrc.sh openstack-tools
```

## With SSH server

With a random port:

```
$ docker run -v $(pwd)/openrc.sh:/root/openrc.sh -d -P --name ostools openstack-tools-with-ssh
$ docker port ostools 22
0.0.0.0:49154
```

On a specific port:

```
$ docker run -v $(pwd)/openrc.sh:/root/openrc.sh -d -p 0.0.0.0:49154:22 --name ostools openstackclient-with-ssh
```

Connect on the published SSH port with root and `ostools@` password :

```
$ ssh root@DOCKERHOST_IP -p 49154
password: ostools@
```

# Openstack tools tests

You can test the `openstack` command:

```
$ . ~/openrc.sh
Please enter your OpenStack Password:
$ openstack image list
```

... should return a list of available templates to deploy as VM.
