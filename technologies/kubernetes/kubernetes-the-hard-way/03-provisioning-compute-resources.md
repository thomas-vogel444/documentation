# Provisioning Compute Resources

## Networking
- Create a `kubernetes-the-hard-way` VPC for the Kubernetes Cluster
```bash
gcloud compute networks create kubernetes-the-hard-way --subnet-mode custom
```

- Create a `kubernetes` subnet in the `kubernetes-the-hard-way` VPC
```bash
gcloud compute networks subnets create kubernetes \
  --network kubernetes-the-hard-way \
  --range 10.240.0.0/24
```

## Firewall Rules
- Add Firewall rules to allow internal communication between instances on all protocols
```bash
gcloud compute firewall-rules create kubernetes-the-hard-way-allow-internal \
  --allow tcp,udp,icmp \
  --network kubernetes-the-hard-way \
  --source-ranges 10.240.0.0/24,10.200.0.0/16
```

- Add Firewall rules to allow external SSH, ICMP, and HTTPS
```bash
gcloud compute firewall-rules create kubernetes-the-hard-way-allow-external \
  --allow tcp:22,tcp:6443,icmp \
  --network kubernetes-the-hard-way \
  --source-ranges 0.0.0.0/0
  ```

## Public IP
- Allocate a static IP address to the external load balancer fronting the K8s servers
```bash
gcloud compute addresses create kubernetes-the-hard-way \
  --region $(gcloud config get-value compute/region)
```

## Kubernetes Controllers

- Create 3 compute instances to host the Kubernetes control plane
```bash
for i in 0 1 2; do
  gcloud compute instances create controller-${i} \
    --async \
    --boot-disk-size 200GB \
    --can-ip-forward \
    --image-family ubuntu-1804-lts \
    --image-project ubuntu-os-cloud \
    --machine-type n1-standard-1 \
    --private-network-ip 10.240.0.1${i} \
    --scopes compute-rw,storage-ro,service-management,service-control,logging-write,monitoring \
    --subnet kubernetes \
    --tags kubernetes-the-hard-way,controller
done
```

## Kubernetes Workers

- Create 3 compute instances to act as Worker nodes. 
```bash
for i in 0 1 2; do
  gcloud compute instances create worker-${i} \
    --async \
    --boot-disk-size 200GB \
    --can-ip-forward \
    --image-family ubuntu-1804-lts \
    --image-project ubuntu-os-cloud \
    --machine-type n1-standard-1 \
    --metadata pod-cidr=10.200.${i}.0/24 \
    --private-network-ip 10.240.0.2${i} \
    --scopes compute-rw,storage-ro,service-management,service-control,logging-write,monitoring \
    --subnet kubernetes \
    --tags kubernetes-the-hard-way,worker
done
```

Note:
- The Kubernetes cluster CIDR range from which the pods on the node will have their cluster IP comes from `metadata pod-cidr`

## Configure SSH Access

Configure SSH access
```bash
gcloud compute ssh controller-0
```















