# Scenario 4: Reclaim Policy Misconfiguration

## Issue
A `Delete` reclaim policy on a PersistentVolume (PV) causes the PV to be deleted when the associated PersistentVolumeClaim (PVC) is deleted, resulting in potential data loss.

## Observations
- **PVC Status:** `Bound` (initially) → Deleted.
- **PV Status:** `Available` (initially) → Deleted.

## Cause
- The `Delete` reclaim policy automatically deletes the PV when the PVC is removed.

## Solution
- Use the `Retain` reclaim policy to prevent accidental data loss. This requires manual management of the PV lifecycle.

## Key Takeaways
- A `Delete` reclaim policy can lead to unintended data loss if not carefully managed.
- Always use the `Retain` policy for critical or persistent data.

## Commands Used
- Deploy resources:
  ```bash
  kubectl apply -f manifests/reclaim-policy-misconfiguration.yaml
## Observations After Deletion

- **`pv-reclaim-policy`:** Successfully deleted after the associated PVC was removed.
- **`pv-storage-exhaustion`:** Entered the `Released` state due to the `Retain` reclaim policy, requiring manual cleanup and reset.

## Lessons Learned

- **Reclaim Policy Behavior:** `Delete` policies require provisioners to clean up associated storage; manual intervention may be necessary if this does not happen.
- **Manual Management for Retain Policy:** For PVs with `Retain` reclaim policy, administrators must clean up data and reset the PV to make it reusable.
- **Data Cleanup:** Always ensure that the underlying storage is cleared when releasing or deleting PVs.

## Commands Used

- Delete PV:
  ```bash
  kubectl delete pv pv-reclaim-policy

