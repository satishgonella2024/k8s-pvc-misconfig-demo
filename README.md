## Scenarios
1. [Storage Exhaustion](docs/storage-exhaustion.md): Demonstrates the impact of a PVC requesting more storage than available on the PV.
2. [Access Mode Mismatch](docs/access-mode-mismatch.md): Demonstrates the impact of mismatched access modes between PVCs and PVs.
3. [Binding Issues](docs/binding-issues.md): Demonstrates the impact of label mismatches between PVCs and PVs.
4. [Reclaim Policy Misconfiguration](docs/reclaim-policy-misconfiguration.md): Demonstrates the risks of using a `Delete` reclaim policy.
5. [Orphaned PVCs](docs/orphaned-pvcs.md): Demonstrates the issue of PVCs remaining bound after Pods are deleted.
