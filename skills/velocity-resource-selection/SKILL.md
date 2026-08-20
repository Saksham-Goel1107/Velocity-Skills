---
name: velocity-resource-selection
description: Automated hardware resource selection guidelines for matching user workloads to optimal CPU, RAM, Disk, and GPU configurations on Velocity.
---

# Velocity Resource Selection Skill

This skill enables AI agents to evaluate project requirements and select optimal container specifications when calling create_workspace.

## Workload Allocation Matrix

| Workload Type | vCPU | RAM | NVMe Storage | GPU Model | Subscription Plan |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Small JS / TS Script / HTML** | 1 | 1 GB | 5 GB | 'none' | FREE / PRO |
| **Standard React / Next.js / Python App** | 2 | 4 GB | 10 GB | 'none' | FREE / PRO |
| **Large Monorepo Build / Rust / Go Compilation** | 4 | 8 GB | 10 GB | 'none' | FREE / PRO |
| **ML Inference / PyTorch Small Models** | 4 | 8 GB | 10 GB | 'rtx4090' | PRO required |
| **Stable Diffusion / Media Generation** | 4 | 8 GB | 10 GB | 'rtx5090' / 'rtx6000' | PRO required |
| **LLM Fine-Tuning / Large AI Training** | 4 | 8 GB | 10 GB | 'h100' / 'h200' | PRO required |

## Decision Rules

1. **Discrete Value Enforcement**:
   - cpu: Only 1, 2, or 4.
   - memory: Only 1, 2, 4, or 8 GB.
   - disk: Only 5 or 10 GB.
2. **GPU Feature Requirement**:
   - GPUs require a **Pro Plan**. If user is on Free Plan, restrict to CPU-only or prompt user to upgrade to Pro.
3. **Cost Efficiency**:
   - Always choose the minimal hardware allocation capable of fulfilling the workload to minimize metered billing burn rate.
