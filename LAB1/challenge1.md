## Persistent Volume (PV)
Create a **Persistent Volume** named `log-volume` with the following specifications:
- **Storage Class Name:** `manual`
- **Access Mode:** `RWX` (ReadWriteMany)
- **Size:** `1Gi`
- **Host Path:** `/opt/volume/nginx`

## Persistent Volume Claim (PVC)
Define a **Persistent Volume Claim** named `log-claim`:
- **Minimum Storage Request:** `200Mi`
- **Bound to:** `log-volume`

## Pod Configuration
Deploy a **Pod** named `logger`:
- **Image:** `nginx:alpine`
- **Volume Mount Location:** `/var/www/nginx`