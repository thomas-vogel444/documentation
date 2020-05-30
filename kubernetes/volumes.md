# Volumes

From https://kubernetes.io/docs/concepts/storage/volumes/

2 problems need solving when running multiple containers within a Pod:
- restarted containers lose their files
- files need to be shared across containers

The Volume abstraction solves both these problems

## Background

In Docker, a Volume is merely a directory on disk whose lifetime isn't managed.

In Kubernetes:
- a Volume has an explicit lifetime -> the same as the Pod that encloses it. 
- a Volume is just a directory which is accessible to the containers within a Pod.

When specifying Volumes, you need to set 2 things:
- what volume to provide for the Pod
- where to mount the volume within the containers

## Types of Volume

There are many types of Volumes:
- emptyDir
    - contents are erased once the Pod is deleted
- configMap
    - a way to inject configuration data into Pods
    - The data stored in a `ConfigMap` object can be references in a volume of type `configMap`
- secret
    - a way to inject secrets, such as passwords and tokens
- downwardAPI
- projected
- persistentVolumeClaim
- awsElasticBlockStore
- azureDisk
- azureFile
- cephfs
- cinder
- csi
- fc (fibre channel)
- flexVolume
- flocker
- gcePersistentDisk
- gitRepo (deprecated)
- glusterfs
- hostPath
- iscsi
- local
- nfs
- portworxVolume
- quobyte
- rbd
- scaleIO
- storageos
- vsphereVolume
