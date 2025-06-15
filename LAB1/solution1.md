# Solution file for LAB1/Challenge1:
### Kubernetes Persistent Volume Explained

#### Overview
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

