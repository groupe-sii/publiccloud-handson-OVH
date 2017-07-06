This document helps to provision a specific number of containers to host a hands'on meeting and provide SSH access to a pre-configured system.

SSH ports are published counting from 50001.

Containers are named according to the `containername` prefix.

# Docker host

    ... to complete...

# Docker containers

    nbcontainers=12
    containername="handson_tests"

    for i in `seq -w 1 $nbcontainers` ; do
        docker run -v $(pwd)/openrc.sh:/root/openrc.sh -d -p 0.0.0.0:500$i:22 --name $containername-$i openstackclient
    done

# Clean docker containers

    for i in `seq -w 1 $nbcontainers` ; do
        docker rm -f $containername-$i
    done
