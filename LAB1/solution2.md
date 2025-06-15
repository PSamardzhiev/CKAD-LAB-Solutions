## Challenge 2 - Solution
Incoming or outgoing connections are not working because of network policy. In the default namespace, we deployed a default-deny network policy which is interrupting the incoming or outgoing connections.\
To check the existing network policies you can execute the below command:
```bash
kubectl get networkpolicies
```

Now, create a network policy called test-network-policy (or use any other name) to allow the connections, as follows:
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      run: secure-pod
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          name: webapp-color
    ports:
    - protocol: TCP
      port: 80
```
Then check the connectivity from the webapp-color pod to the secure-pod:\
```bash
kubectl exec -it webapp-color -- sh
## inside the container type the below command:
nc -v -z -w 5 secure-service 80
## the console should return that the port is now open
```