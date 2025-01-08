# Scenario 3: Binding Issues

## Issue
A PersistentVolumeClaim (PVC) uses label selectors to match a PersistentVolume (PV). If the labels do not match, the PVC remains in a `Pending` state, and the dependent pod cannot start.

## Observations
- **PVC Status:** `Pending`
- **Pod Status:** `Pending`
- **PVC Events:**
  ```
  Normal  FailedBinding  persistentvolume-controller  no matching persistent volume found for PVC
  ```
- **Pod Events:**
  ```
  Warning  FailedScheduling  default-scheduler  0/3 nodes are available: pod has unbound immediate PersistentVolumeClaims.
  ```

## Cause
- The PVC specifies a selector with the label `storage-tier: silver`, but the available PV has the label `storage-tier: gold`.

## Solution
- Update the **PVC** to match the labels of the available **PV** (`storage-tier: gold`), or
- Update the **PV** to include the label `storage-tier: silver`.

## Key Takeaways
- Label mismatches in PVC selectors prevent PVC binding and pod deployment.
- Always ensure label selectors in PVCs match the labels on PVs.

## Commands Used
- Deploy resources:
  ```bash
  kubectl apply -f manifests/binding-issues.yaml
  ```
- Check PVC status:
  ```bash
  kubectl get pvc
  kubectl describe pvc pvc-binding-issues
  ```
- Check Pod status:
  ```bash
  kubectl get pod
  kubectl describe pod pod-binding-issues
  ```

