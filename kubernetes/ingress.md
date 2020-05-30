# Ingresses

From https://blog.getambassador.io/kubernetes-ingress-nodeport-load-balancers-and-ingress-controllers-6e29f1c44f2d

Kubernetes uses 3 approaches to expose your application to the outside world
- A Kubernetes Service of type NodePort exposing the application on a port across each node
- A Kubernetes Service of type LoadBalancer, which creates an external load balancer pointing to your Kubernetes service in your cluster.
- A Kubernetes Ingress Resource

## NodePort

- opens a port on each node of your cluster. All incoming traffic on the NodePort is routed to the service
- NodePort is assigned from a non-standard port range
- Useful for development purposes and as a building block for other ingress methods

## LoadBalancer

- deploys an external load balancer specific to the cloud provider associated with a specific IP address routing incoming requests to your service

## Ingress Resource

- creates a Ingress resource allowing URL based HTTP routing

