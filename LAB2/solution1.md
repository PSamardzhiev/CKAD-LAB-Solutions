## Challenge 1 - Solution
use 
```bash
kubectl get po -n dev1401 nginx1401 -oyaml >> pod.yaml
```
Then open the YAML file with vi or any text editor\
Apple the changes shown below with the YAML comments!
```bash
# Look for comments such as this text in the below YAML file which explains how this challenge is solved!
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    cni.projectcalico.org/containerID: 3d623c090c0d5619230fe23750150fad8ddbc19ef94d99cb40b35dbca52ff130
    cni.projectcalico.org/podIP: 172.17.1.2/32
    cni.projectcalico.org/podIPs: 172.17.1.2/32
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"creationTimestamp":null,"labels":{"run":"nginx"},"name":"nginx1401","namespace":"dev1401"},"spec":{"containers":[{"image":"kodekloud/nginx","imagePullPolicy":"IfNotPresent","name":"nginx","ports":[{"containerPort":9080}],"readinessProbe":{"httpGet":{"path":"/","port":8080}},"resources":{}}],"dnsPolicy":"ClusterFirst","restartPolicy":"OnFailure"},"status":{}}
  labels:
    run: nginx
  name: nginx1401
  namespace: dev1401
spec:
  containers:
  - image: kodekloud/nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    ports:
    - containerPort: 9080
      protocol: TCP
    readinessProbe:
      failureThreshold: 3
      httpGet:
        path: /
        port: 9080 ## This should match the - ContainerPort: 9080 - so this is the FIX!
        scheme: HTTP
      periodSeconds: 10
      successThreshold: 1
      timeoutSeconds: 1
    livenessProbe: # <--- begin changes as per the requirements from the task!
      exec:
        command:
          - ls
          - /var/www/html/file_check
      initialDelaySeconds: 10
      periodSeconds: 60 # <-- END of changes as per requirements from the task!
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-477gg
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: node01
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: OnFailure
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-477gg
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2025-06-22T16:29:58Z"
    status: "True"
    type: PodReadyToStartContainers
  - lastProbeTime: null
    lastTransitionTime: "2025-06-22T16:29:50Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2025-06-22T16:29:50Z"
    message: 'containers with unready status: [nginx]'
    reason: ContainersNotReady
    status: "False"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2025-06-22T16:29:50Z"
    message: 'containers with unready status: [nginx]'
    reason: ContainersNotReady
    status: "False"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2025-06-22T16:29:50Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://3ee87a72f6da9d123016e6b5b1795e0c6ef4e4c893f496c17370ccfa90af415f
    image: docker.io/kodekloud/nginx:latest
    imageID: docker.io/kodekloud/nginx@sha256:2862900861517dfaf9e0ed0f4fa199744a7410f4f78520866031c725c386bb5e
    lastState: {}
    name: nginx
    ready: false
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2025-06-22T16:29:58Z"
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-477gg
      readOnly: true
      recursiveReadOnly: Disabled
  hostIP: 192.168.163.56
  hostIPs:
  - ip: 192.168.163.56
  phase: Running
  podIP: 172.17.1.2
  podIPs:
  - ip: 172.17.1.2
  qosClass: BestEffort
  startTime: "2025-06-22T16:29:50Z"