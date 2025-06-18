## Challenge 4 - Solution
Run the following command to create a manifest for deployment nginx-deploy and save it into a file:

```bash
kubectl create deployment nginx-deploy --image=nginx:1.16 --replicas=4 --dry-run=client -oyaml > nginx-deploy.yaml
```

and add the strategy field under the ***spec*** section as follows:

```yaml
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
```

So final manifest file for deployment called nginx-deploy should looks like below:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deploy
  name: nginx-deploy
  namespace: default
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginx-deploy
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: nginx-deploy
    spec:
      containers:
      - image: nginx:1.16
        imagePullPolicy: IfNotPresent
        name: nginx
```

then run the below command

```bash

kubectl apply -f 

```

nginx-deploy.yaml to create a deployment resource.

Now, upgrade the deployment's image version using the kubectl set image command:

```bash
kubectl set image deployment nginx-deploy nginx=nginx:1.17
```

Run the

```bash
kubectl rollout undo deployment nginx-deploy
```

command to undo the update and go back to the previous version