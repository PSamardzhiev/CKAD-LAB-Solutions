### Solution file for LAB1 - Challenge1:


A **PersistentVolume (PV)** in Kubernetes is a storage resource that provides a way for pods to store and retrieve data beyond their lifecycle. Below is a breakdown of a **PV configuration** using a `hostPath` for local storage.

---
```yaml
# Persistnt Volume Configuration file
apiVersion: v1
kind: PersistentVolume
metadata:
  name: log-volume
spec:
  storageClassName: manual
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/opt/volume/nginx"
```
A **PersistentVolumeClaim (PVC)** in Kubernetes allows a pod to request storage from an existing PersistentVolume (PV). Below is the configuration for a PVC that binds to the `log-volume` created in the previous step.

---

```yaml
# Persistent Volume Claim Configuration file
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: log-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 200Mi
```
---
```yaml
# Deploy Pod name logger with image nginx:alpine which makes use of the PV/PVC created in the previous steps
#
apiVersion: v1
kind: Pod
metadata:
  name: logger
spec:
  containers:
    - name: nginx-container
      image: nginx:alpine
      volumeMounts:
        - name: log-storage
          mountPath: "/var/www/nginx"
  volumes:
    - name: log-storage
      persistentVolumeClaim:
        claimName: log-claim
```