Your output shows that the PVC is in a `Pending` state because no Persistent Volume (PV) is available that matches the PVC's requirements, and no `StorageClass` is set. This is the expected behavior for the **Storage Exhaustion** scenario. Let’s document and proceed:

---

### **Analysis of the Issue**
- **Problem:**
  - The PVC is requesting `2Gi` of storage, but the only PV available (`pv-storage-exhaustion`) has a capacity of `1Gi`.
  - No `StorageClass` is set, so the PVC cannot dynamically provision storage.
  
- **Observation:**
  - PVC status is `Pending`.
  - The associated pod (`pod-storage-exhaustion`) is also in `Pending` state because it cannot mount the unbound PVC.

---

### **Document the Results**
1. Create a documentation file for this scenario:
   ```bash
   touch docs/storage-exhaustion.md
   ```

2. Add the following content to `docs/storage-exhaustion.md`:
   ```markdown
   # Scenario 1: Storage Exhaustion

   ## Issue
   A PersistentVolumeClaim (PVC) requests more storage than is available in the associated PersistentVolume (PV), leading to a `Pending` state for both the PVC and the dependent pod.

   ## Observations
   - **PVC Status:** `Pending`
   - **Pod Status:** `Pending`
   - **PVC Events:**
     ```
     Normal  FailedBinding  persistentvolume-controller  no persistent volumes available for this claim and no storage class is set
     ```

   ## Cause
   - The PVC requests `2Gi` of storage, but the PV has only `1Gi` available.
   - No `StorageClass` is set, so dynamic provisioning is not attempted.

   ## Solution
   To resolve this:
   1. Increase the PV capacity to at least `2Gi`, or
   2. Modify the PVC to request only `1Gi` of storage.

   ## Key Takeaways
   - Always ensure PVC requests align with PV capacities.
   - Use `StorageClass` for dynamic provisioning in production environments.

   ## Commands Used
   - Deploy the resources:
     ```bash
     kubectl apply -f manifests/storage-exhaustion.yaml
     ```
   - Check PVC status:
     ```bash
     kubectl get pvc
     ```
   - Describe PVC:
     ```bash
     kubectl describe pvc pvc-storage-exhaustion
     ```
   ```

---
