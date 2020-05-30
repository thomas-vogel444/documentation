# Cheatsheet for creating Kubernetes clusters in KOPS

### Prerequisite

`export KOPS_STATE_STORE=s3://extended.prism.kops.state`
`export AWS_PROFILE=personal`

### Commands overview

Kops commands
- create
     Creates KOPS resources without applying them.
     To apply the resources, use "kops update cluster"
- replace
    Replace a cluster desired configuration using a YAML file
- rolling-update
- set
    Set a configuration field.
    kops set does not update the cloud resources, to apply the changes use "kops update cluster".
- update
    Applies the changes to the cluster.
- upgrade
    Automates checking for and applying Kubernetes updates. This upgrades a cluster to the latest recommended production ready k8s version. After this command is run, use kops update cluster and kops rolling-update cluster to finish a cluster upgrade.

### Examples

Create the Cluster + InstanceGroups config file

`kops create cluster --name extendedprism.com --zones eu-west-1a,eu-west-1b,eu-west-1c --master-size t2.micro --master-count 1 --node-size t2.large --node-count 2 --dry-run -o yaml > extendedprism-cluster.yaml`

Create the actual cluster

`kops update cluster extendedprism.com --yes`

Update a cluster from file

`kops replace -f extendedprism-cluster.yaml`

`kops update cluster --yes`

`kops rolling-update cluster`

