---
name: velocity-troubleshooting
description: Known failure modes, error recovery procedures, and diagnostic steps for Velocity cloud containers.
---

# Velocity Troubleshooting Skill

This skill equips AI agents to diagnose runtime issues, inspect failure notifications, and execute recovery procedures.

## Known Failure Modes & Recovery Matrix

1. CREATING or PROVISIONING Stuck:
   - Cause: Daytona container creation delay.
   - Action: Wait 10s and re-check list_workspaces. Do not call create_workspace again.

2. FAILED Status:
   - Cause: Exceeded memory cap (>8GB) or image build failure.
   - Action: Call get_notifications to read error details. Re-create workspace with memory 8 GB or less.

3. 403 PREMIUM_FEATURE_LOCKED:
   - Cause: GPU allocation requested on Free Plan.
   - Action: Check get_analytics_metrics. Switch gpu to none or prompt user to upgrade to Pro plan.

4. 403 INSUFFICIENT_BALANCE:
   - Cause: Depleted wallet balance (.00).
   - Action: Prompt user to recharge wallet before starting/creating containers.

5. Connection Preview URL Unavailable:
   - Cause: Container is STOPPED or app server not bound to 0.0.0.0.
   - Action: Call start_workspace and ensure app binds to 0.0.0.0.
