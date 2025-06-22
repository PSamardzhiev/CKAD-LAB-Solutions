## Challenge2 - Solution

The solution is written in the YAML file below:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: dice
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      backoffLimit: 25
      parallelism: 0
      activeDeadlineSeconds: 20
      completions: 1
      template:
        spec:
          containers:
          - name: throw-dice
            image: kodekloud/throw-dice
            imagePullPolicy: IfNotPresent
          restartPolicy: Never
```
