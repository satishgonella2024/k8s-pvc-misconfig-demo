# Kubernetes PVC Misconfiguration Demo
This project demonstrates common PVC misconfigurations in Kubernetes, their impact, and how to recover from them. Each scenario is accompanied by observability insights and best practices.
## Scenarios
1. [Storage Exhaustion](docs/storage-exhaustion.md): Demonstrates the impact of a PVC requesting more storage than available on the PV.
2. [Access Mode Mismatch](docs/access-mode-mismatch.md): Demonstrates the impact of mismatched access modes between PVCs and PVs.
3. [Binding Issues](docs/binding-issues.md): Demonstrates the impact of label mismatches between PVCs and PVs.

