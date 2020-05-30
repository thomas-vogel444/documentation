# Notes

- How to run a pod from Docker Hub?
- Changing existing resources:
    - kubectl set ...
    - kubectl edit ...
- For more info: `kubectl get pods -o wide`
- Getting Logs: `kubectl logs nginx`
- Customs columns: `kubectl get pods -o=custom-columns="POD_NAME:.metadata.name"`