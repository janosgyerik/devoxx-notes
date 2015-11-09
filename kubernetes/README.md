# Kubernetes

Container cluster manager from Google
http://kubernetes.io/

https://github.com/kubernetes/kubernetes

## Concepts

- pods: collocated group of Docker containers that share an IP and storage volume
  + one container ~ one pod

- service: single, stable name for a set of pods, also acts as LB

- label: used to organize and select group of objects

- replication controller: manages the lifecycle of pods and ensures specified number are running

- node: ...
  + On each node, there can be multiple pods running.
  + one node ~ one pod

- master: ...

- etcd: ...
  + distributed key-value store of/for ...

Needs Vagrant or other provider.

## `kubectl`

- `kubectl get pods` or nodes, or service, or rc (replication controllers)

## Example config

    apiVersion: v1
    kind: Pod
    metadata:
      name: wildfly-pod
      labels:
        name: wildfly
      spec:
        containers:
          - image: jboss/wildfly
            name: wildfly-pod
            ports:
              - containerPort: 8080

export KUBERNETES_PROVIDER=vagrant
/path/to/kubernetes/kube-ctl.sh up

## Replication controller

- recommended to wrap nodes and services in rc
- pods should be set `Restart=Always` (the default)

Scaling up:

    kubectl.sh scale --replicas=3 rc wildfly-rc

## Health checks

- Replication controller can check the status and automatically restart pods when they go down

## Kubernetes using Docker

Layers:

- OSX
  - Docker Machine
    - Kubernetes (Docker Compose)
      - master
        - pod
          - application container
      - proxy
      - etcd

## Docker Swarm vs Kubernetes

https://github.com/javaee-samples/docker-java/blob/master/chapters/docker-vs-kubernetes.adoc

## Misc

- CoreOS: can run containers natively
