## Challenge 5
Create a redis deployment with the following parameters:

Name of the deployment should be redis using the redis:alpine image. It should have exactly 1 replica.

The container should request for .2 CPU. It should use the label app=redis.

It should mount exactly 2 volumes.

a. An Empty directory volume called data at path /redis-master-data.

b. A configmap volume called redis-config at path /redis-master.

c. The container should expose the port 6379.


The configmap has already been created - the manifest file is listed below:
```yaml
apiVersion: v1
data:
  redis-config: |
    maxmemory 2mb
    maxmemory-policy allkeys-lru
kind: ConfigMap
metadata:
  creationTimestamp: "2025-06-21T17:13:01Z"
  name: redis-config
  namespace: default
  resourceVersion: "2785"
  uid: 4fc4e4a6-0bc0-4b28-b0fb-c2a05f06765e
```
