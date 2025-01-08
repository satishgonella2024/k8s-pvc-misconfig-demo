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

## Observations After Pod Deletion

- **PVC Status:** Remained `Bound` after the Pod was deleted, consuming the associated PV.
- **PV Status:** Remained `Bound` to the PVC due to the `Retain` reclaim policy, making the storage unavailable for reuse.

## Solution

1. Manually delete the orphaned PVC:
   ```bash
   kubectl delete pvc pvc-orphaned-pvcs
