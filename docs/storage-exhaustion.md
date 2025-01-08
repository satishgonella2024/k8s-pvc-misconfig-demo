
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

---
