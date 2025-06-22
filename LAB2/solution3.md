## Challenge 3 - Solution

The solution is written in the YAML file below
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: my-busybox
  namespace: dev2406
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
                - controlplane
  volumes:
    - name: secret-volume
      secret:
        secretName: dotfile-secret
  containers:
  - image: busybox
    name: secret
    command:
    - sleep
    - "3600"
    volumeMounts:
      - name: secret-volume
        readOnly: true
        mountPath: /etc/secret-volume
```