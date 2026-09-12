---
name: velocity-sdk-and-cli
description: TypeScript SDK (@fairarena/velocity-cloud-sandbox) and CLI (velocitycloudsandbox) syntax, initialization, and remote container control.
---

# Velocity TypeScript SDK & CLI Skill

Complete guide for programmatically creating sandboxes, executing remote terminal commands, and controlling infrastructure via TypeScript SDK or CLI.

- **Live Documentation**: https://velocity-docs.fairarena.app/#sdk-docs
- **Machine-Readable Spec**: https://velocity-docs.fairarena.app/sdk-llms.txt

---

## 1. Package Installation

`ash
npm install @fairarena/velocity-cloud-sandbox
npm install -g @fairarena/velocity-cloud-sandbox-cli
`

---

## 2. TypeScript SDK Usage

` ypescript
import { VelocityCloudSandbox } from @fairarena/velocity-cloud-sandbox;

const velocity = new VelocityCloudSandbox({
apiKey: process.env.VELOCITY_API_KEY,
});

const sandbox = await velocity.createSandbox({
repo: github.com/Saksham-Goel1107/Velocity,
cpu: 4,
memoryGB: 8,
diskGB: 10,
gpu: rtx5090,
gpuCount: 1,
editor: code-server,
customName: AI Dev Sandbox,
autoStop: 15,
});

const execResult = await sandbox.exec(pnpm install && pnpm build);
console.log(execResult.stdout);

await sandbox.stop();
await sandbox.start();
await sandbox.delete();
`

---

## 3. CLI Terminal Commands

`ash
export VELOCITY_API_KEY=ak_live_your_key

velocitycloudsandbox create --repo Saksham-Goel1107/Velocity --cpu 4 --ram 8 --gpu rtx5090
velocitycloudsandbox exec --id ws_123456 --cmd pnpm test
velocitycloudsandbox list
velocitycloudsandbox status
`
