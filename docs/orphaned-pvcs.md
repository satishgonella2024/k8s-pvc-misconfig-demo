# Scenario 5: Orphaned PVCs

## Issue
PersistentVolumeClaims (PVCs) that are not deleted after their associated applications are removed remain `Bound`, unnecessarily consuming storage.

## Observations
- **Initial State:**
  - PVC `pvc-orphaned-pvcs` was `Bound` to PV `pv-orphaned-pvcs`.
  - Pod `pod-orphaned-pvcs` was in the `Running` state, using the PVC.
- **After Pod Deletion:**
  - PVC `pvc-orphaned-pvcs` remained `Bound`, consuming the PV.
  - PV `pv-orphaned-pvcs` remained `Bound` to the PVC, leaving the storage unavailable for reuse.

## Cause
- PVCs are not automatically deleted when their associated Pods or applications are removed.

## Solution
1. Manually delete the orphaned PVCs to free up storage resources:
   ```bash
   kubectl delete pvc pvc-orphaned-pvcs
   
2. Reset or delete the PV:
   - **Reset the PV for reuse**:
     ```bash
     kubectl patch pv pv-orphaned-pvcs -p '{"spec":{"claimRef": null}}'
     ```
   - **Delete the PV**:
     ```bash
     kubectl delete pv pv-orphaned-pvcs
     ```

## Lessons Learned
- Orphaned PVCs unnecessarily consume cluster resources.
- Automate cleanup tasks or use owner references to ensure PVCs are deleted with dependent applications.
- Regular audits of PVC and PV resources can prevent storage mismanagement.

## Commands Used
- **Deploy resources**:
  ```bash
  kubectl apply -f manifests/orphaned-pvcs.yaml
  ```
- **Delete Pod**:
  ```bash
  kubectl delete pod pod-orphaned-pvcs
  ```
- **Delete PVC**:
  ```bash
  kubectl delete pvc pvc-orphaned-pvcs
  ```
- **Delete PV**:
  ```bash
  kubectl delete pv pv-orphaned-pvcs
  ```

---
