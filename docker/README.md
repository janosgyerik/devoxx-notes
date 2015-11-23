## Docker Toolbox

- Docker Client
- Docker Machine -- next gen VM, not yet production ready
- Docker Compose -- define and run multi-container applications
- Docker Kinematic
- Boot2Docker -- deprecated in favor of Docker Machine
- ?

## Examples

Example 1:

    FROM fedora:latest

    CMD echo 'hello world'

Example 2:

    FROM jboss/wildfly

    RUN curl -L https://github.com/javaee-samples/javaee7-hol/raw/master/solution/movieplex7-1.0-SNAPSHOT.war -o /opt/jboss/wildfly/standalone/deployments/movieplex7-1.0-SNAPSHOT.war

## Work

docker-machine create -d=virtualbox devoxx

## Memo

A tiny Linux VM:

     ls -lh ~/.docker/machine/cache/
    total 61440
    -rw-r--r--  1 janos  staff    30M Nov  9 09:43 boot2docker.iso

Env variables to setup when working with an image:

    docker-machine env devoxx

    eval $(docker-machine env devoxx)

Misc:

    # list images
    docker images

    # list processes
    docker ps

"docker containers are like diapers: you shit in them and throw away"

    eval "$(docker-machine env devoxx)"

    docker run -it ubuntu sh

    docker run -it -p 8080:8080 jboss/wildfly

    curl $(docker-machine ip devoxx):8080

    docker run
    --name mysqldb
    -e MYSQL_USER=mysql
    -e MYSQL_PASSWORD=..
    -e MYSQL_DATABASE=..
    -e MYSQL_ROOT_PASSWORD=..
    -d
    mysql

Dockerfile -- default filename for configuring a Docker image (in a dir)

## Docker Compose

- docker-compose.yml
- docker-compose.override.yml
  + can override whatever was in docer-compose.yml
    using: `docker-compose up -d`
- multiple files specified using -f
- all paths relative to base config file

Example using linking:

    mysqldb:
      image: mysql
      environment:
        MYSQL_DATABASE: sample
        MYSQL_USER: ...
        ...
    mywildfly:
      image: arungupta/wildfly-mysql-javaee7
      links:
        - mysqldb:db

Example using networking:

    mysqldb:
      container_name: "db"
      image: mysql
      environment:
        MYSQL_DATABASE: sample
        MYSQL_USER: ...
        ...
    mywildfly:
      image: arungupta/wildfly-mysql-javaee7
      environment:
        - MYSQL=db
      ports:
        - 3306:3306

Example:

    couchbase1:
      image: couchbase/server
      volumes:
        - ~/couchbase/node1:/opt/couchbase/var
    couchbase2:
      image: couchbase/server
      volumes:
        - ~/couchbase/node2:/opt/couchbase/var
    couchbase3:
      image: couchbase/server
      volumes:
        - ~/couchbase/node3:/opt/couchbase/var
      ports:
        - 8091:8091
        - 8092:8092
        - 8093:8093
        - 11210:11210

## Multi host networking

- create virtual networks and attach containers
- bridge network: span a single host
- overlay network: span multiple hosts
- works with Swarm and Compose (experimental)
- pluggable: Calico, Cisco, Weave, ...

## Networking vs links

- connect containers to each other across different physical or virtual hosts
- links: reliance on env variables did not work very well

Compose a config from multiple files, each overriding previous:

    docker-compose up
    -f docker-compose.yml
    -f production.yml
    -d

## Docker Swarm

- native clustering
- unified interface to a pool of Docker hosts
- fully integrated with Machine and Compose

One machine can be part of one cluster only.

## Master high availability

- handle failover
- primary manager, multiple replica instances
- requests to replicate are proxied to primary
- `docker run swarm manage`
  + `--replication`: enable Swarm manager replication (not default)
  + `--replication-ttl "30s"`
  + ...

## Scheduling

Based on CPU (`-d`), RAM (`-m`), number of containers

    docker-machine create --strategy spread
    docker-machine create --strategy binpack  # node with most number of running containers
    docker-machine create --strategy random  # chaos monkey
    docker run --help | grep cpu

## Persistent storage

Data volumes -- used to persist data indendent from container lifecycle

    docker volume --help

Plugins: Flocker, Ceph, ...

    docker run -it -v data ....

## Networking

    docker network --help

## Multi-cloud deployments

For example, you can have any app call any db on any cloud. (How?)

## Links

- https://github.com/javaee-samples/docker-java/blob/master/chapters/
- https://github.com/javaee-samples/docker-java/blob/master/chapters/docker-commands.adoc
