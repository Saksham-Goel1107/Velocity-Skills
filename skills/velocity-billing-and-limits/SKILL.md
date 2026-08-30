---
name: velocity-billing-and-limits
description: Single canonical pricing reference, metered per-second billing formulas, wallet balance rules, Razorpay checkout, and subscription tiers.
---

# Velocity Billing & Limits Skill

Canonical pricing reference and metered per-second billing formulas for Velocity Cloud Sandboxes.

- **Live Documentation**: https://velocity-docs.fairarena.app/#api-auth-docs
- **Machine-Readable Spec**: https://velocity-docs.fairarena.app/llms.txt

---

## 1. Per-Second Metered Pricing Matrix

| Compute Specification | Hourly Rate (USD) | Per-Second Nano Rate (USD) |
| :--- | :--- | :--- |
| **1 vCPU, 1 GB RAM (Lite)** | .012 / hr | .00000333 / sec |
| **2 vCPU, 4 GB RAM (Standard)** | .036 / hr | .00001000 / sec |
| **4 vCPU, 8 GB RAM (Performance)** | .080 / hr | .00002222 / sec |
| **Nvidia RTX 4090 GPU (24GB VRAM)** | .280 / hr | .00007778 / sec |
| **Nvidia RTX 5090 GPU (32GB VRAM)** | .450 / hr | .00012500 / sec |
| **Nvidia RTX 6000 Ada GPU (48GB)** | .650 / hr | .00018055 / sec |
| **Nvidia H100 SXM5 GPU (80GB)** | .850 / hr | .00051388 / sec |
| **Nvidia H200 SXM5 GPU (141GB)** | .450 / hr | .00068055 / sec |

---

## 2. Wallet & Billing APIs

- GET /api/billing: Retrieves wallet balance, burn rate, and transactions.
- PUT /api/billing/budget: Sets spending budget.
- POST /api/billing/razorpay/create-order: Generates Razorpay checkout order.
