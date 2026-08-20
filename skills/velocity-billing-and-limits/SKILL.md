---
name: velocity-billing-and-limits
description: Single canonical pricing reference, metered nano-USD billing formula, credit behavior, and capacity limit rules for Velocity.
---

# Velocity Billing & Capacity Limits Skill

This skill provides the single canonical pricing reference and metered billing formulas for Velocity Cloud Sandboxes.

## Canonical Pricing Rates (Per-Second Metered Billing)

Velocity calculates compute costs per second using exact integer arithmetic (1 nano-USD = .000000001):

- **vCPU**: .00001540 / sec  (.05544 / hr)
- **RAM Memory**: .00000495 / sec per GB  (.01782 / hr per GB)
- **NVMe Storage**: .00000033 / sec per GB  (.001188 / hr per GB)
- **GPU Models (Pro Plan Required)**:
  - **RTX 4090**: .00030250 / sec  (.0890 / hr)
  - **RTX 5090**: .00039380 / sec  (.4177 / hr)
  - **RTX 6000**: .00092620 / sec  (.3343 / hr)
  - **H100**: .00120670 / sec  (.3441 / hr)
  - **H200**: .00138710 / sec  (.9936 / hr)

## Cost Calculation Formula
`
Cost (USD/sec) = (cpu_count * 0.00001540)
               + (memory_gb * 0.00000495)
               + (disk_gb * 0.00000033)
               + (gpu_rate_per_sec * gpu_count)
`

## Wallet & Depletion Behavior
1. **Wallet Depletion (.00)**: If walletBalanceNano <= 0, container creation (create_workspace) and container booting (start_workspace) are blocked with a 403 INSUFFICIENT_BALANCE error.
2. **Compute vs Storage Billing**:
   - When a container is **RUNNING**, vCPU, RAM, Disk, and GPU rates bill continuously.
   - When a container is **STOPPED**, vCPU, RAM, and GPU compute billing drops to **.00/sec**. NVMe storage continues billing at half-rate to preserve disk state.
