---

### **Steps for Scenario 2**

#### **1. Create the Manifest**
1. Create a new file for Scenario 2:
   ```bash
   touch manifests/access-mode-mismatch.yaml
   ```

2. Add the following YAML to `manifests/access-mode-mismatch.yaml`:
   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pv-access-mismatch
   spec:
     capacity:
       storage: 1Gi
     accessModes:
       - ReadWriteOnce
     hostPath:
       path: "/mnt/data/pv-access-mismatch"
   ---
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-access-mismatch
   spec:
     resources:
       requests:
         storage: 1Gi
     accessModes:
       - ReadWriteMany  # Mismatched access mode
   ---
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod-access-mismatch
   spec:
     containers:
     - name: app
       image: nginx
       volumeMounts:
       - mountPath: "/usr/share/nginx/html"
         name: storage
     volumes:
     - name: storage
       persistentVolumeClaim:
         claimName: pvc-access-mismatch
   ```

---

#### **2. Apply the Manifest**
Deploy the resources to your cluster:
```bash
kubectl apply -f manifests/access-mode-mismatch.yaml
```

---

#### **3. Observe the Results**
Run the following commands to check the status of the PVC and Pod:
```bash
kubectl get pvc
kubectl describe pvc pvc-access-mismatch
kubectl get pod
kubectl describe pod pod-access-mismatch
```

---

#### **4. Document Observations**
Create a new file for documenting this scenario:
```bash
touch docs/access-mode-mismatch.md
```

Add the following content:
```markdown
# Scenario 2: Access Mode Mismatch

## Issue
A PersistentVolumeClaim (PVC) requests an access mode (`ReadWriteMany`) that is not supported by the associated PersistentVolume (PV), which supports only `ReadWriteOnce`.

## Observations
- **PVC Status:** `Pending`
- **Pod Status:** `Pending`
- **PVC Events:**
  ```
  Normal  FailedBinding  persistentvolume-controller  no matching persistent volume found
  

## Cause
- The PVC's requested access mode does not match the PV's defined access mode.

## Solution
- Modify the PV to support the requested access mode (`ReadWriteMany`), or
- Update the PVC to request the supported access mode (`ReadWriteOnce`).

## Key Takeaways
- Access mode mismatches prevent PVC binding and pod deployment.
- Ensure the access modes align between PVs and PVCs.

## Commands Used
- Deploy the resources:
  ```bash
  kubectl apply -f manifests/access-mode-mismatch.yaml
  ```
- Check PVC status:
  ```bash
  kubectl get pvc
  kubectl describe pvc pvc-access-mismatch
  ```
- Check Pod status:
  ```bash
  kubectl get pod
  kubectl describe pod pod-access-mismatch
  ```

---

