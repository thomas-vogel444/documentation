# Services

## hitting an internal service via DNS

You can send http requests to a service either 
- directly via the Cluster IP 
- via an internal DNS name: `<service-name>.<namespace>.svc.cluster.local`
    - E.g. `service-configs.default.svc.cluster.local`