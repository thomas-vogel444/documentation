# Useful commands for Kubernetes

### Explain

`kubectl explain deployment`

`kubectl explain deployment --recursive`

`kubectl explain deployment.spec.strategy`

### Running a pod from a Docker image

`kubectl run <pod-name> --image=<image-name> generator=run-pod/v1 --command -- <command>`

### Logs

`kubectl logs <pod-name> -c <container name>`

`kubectl logs <pod-name> -c <container name> --previous`

### Verbosity

`kubectl <command> --v 6`

### Port forwarding

Forwards all local traffic on a given port to a pod's specified port. Useful for Development.

`kubectl port-forward <pod-name> <local-port>:<pod-port>`

## Executing commands on a pod

`kubectl attach <pod-name>`

`kubectl exec -it <pod-name> bash`

`kubectl exec <pod-name> env`

`kubectl exec <pod-name> -- curl http://www.google.com`

## Output

### Json format

`kubectl get pods -o jsonpath='...'`

### Columns

`kubectl get pods -o <column1>,<column2>,...`

`kubectl get pods --sort-by <column>`

### Showing labels

`kubectl get pods --show-labels`

`kubectl get pods -L <label-name1>,<label-name2>,...`

### Filtering by label

`kubectl get pods -l <label>=<value>`

`kubectl get pods -l <label>`

`kubectl get pods -l "!<label>"`

`kubectl get pods -l <label> in (<value1>,<value1>)`

`kubectl get pods -l <label> notin (<value1>,<value1>)`

## Namespaces

`kubectl get pods -n <namespace>`

`kubectl get pods -all-namespace`

## Config

Changes the current context's namespace 

`kubectl config set-context $(kubectl config current-context) --namespace <namespace>`

## Modifying a resource

Adds or modifies JSON fields

`kubectl patch deployment <name> -p '{...}'`

`kubectl set image deployment <name> <container-name>=<image-name>`

`kubectl edit <resource-name>`

## Rollouts

`kubectl rollout status deployment <deployment-name>`

`kubectl rollout pause deployment <deployment-name>`

`kubectl rollout resume deployment <deployment-name>`

`kubectl rollout undo deployment <deployment-name>`

`kubectl rollout undo deployment <deployment-name> --to-revision=<revision-number>`

`kubectl rollout history deployment <deployment-name>`