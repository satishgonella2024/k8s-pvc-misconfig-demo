# 📖 Kubernetes PVC Misconfigurations: A Hands-On Guide

Welcome to the **Kubernetes PVC Misconfigurations** guide! Explore the common pitfalls of managing PersistentVolumeClaims (PVCs) and PersistentVolumes (PVs) in Kubernetes through hands-on scenarios.

---

## 🚀 Scenarios Overview

1. **[Storage Exhaustion](docs/storage-exhaustion.md)**  
   🗃️ *Demonstrates the impact of a PVC requesting more storage than available on the PV.*  
   > **Key takeaway**: Ensure PVC requests align with PV capacities to prevent resource contention.

2. **[Access Mode Mismatch](docs/access-mode-mismatch.md)**  
   🔓 *Highlights the impact of mismatched access modes between PVCs and PVs.*  
   > **Key takeaway**: Matching access modes is crucial for successful PVC binding.

3. **[Binding Issues](docs/binding-issues.md)**  
   🏷️ *Explores the effect of label mismatches between PVCs and PVs.*  
   > **Key takeaway**: Labels in PVC selectors must match labels on PVs.

4. **[Reclaim Policy Misconfiguration](docs/reclaim-policy-misconfiguration.md)**  
   🛡️ *Demonstrates the risks of using a `Delete` reclaim policy.*  
   > **Key takeaway**: Use `Retain` for critical data to avoid unintended data loss.

5. **[Orphaned PVCs](docs/orphaned-pvcs.md)**  
   🗑️ *Shows the issue of PVCs remaining bound after Pods are deleted.*  
   > **Key takeaway**: Automate cleanup tasks to manage PVC lifecycles effectively.

---

## 💡 Why Explore These Scenarios?

Managing storage in Kubernetes can be tricky, and small misconfigurations can have a big impact on application stability and resource utilization. These scenarios aim to:

- Enhance your understanding of Kubernetes storage concepts.
- Provide practical troubleshooting steps for common issues.
- Equip you with best practices for managing PVCs and PVs.

---

## 🛠️ Get Started

Click on any scenario above to dive deeper, explore the YAML manifests, and follow step-by-step instructions for hands-on learning!

Happy learning! 🎉
