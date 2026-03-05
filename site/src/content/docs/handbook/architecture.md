---
title: Architecture
description: Three-layer architecture for governance, routing, and attestation.
sidebar:
  order: 2
---

Nexus Suite is structured as three independent layers that can be composed together or used separately.

## Layer overview

```
nexus-control        <-- governance policies, config
    |
nexus-router         <-- request dispatch + routing
    |-- stdout-adapter
    |-- http-adapter
    |-- (custom adapter)
    |
nexus-attest         <-- signature verification
```

## Control layer: nexus-control

The control plane defines and enforces governance policies. This includes:

- **Access rules** -- which tools can be invoked and by whom.
- **Rate limits** -- throttle requests to prevent abuse.
- **Audit trails** -- log every policy decision for compliance.
- **Configuration** -- centralized config that downstream layers consume.

nexus-control sits at the top of the stack. It feeds policy decisions into the routing layer.

## Routing layer: nexus-router

The router dispatches incoming requests to the correct tool via pluggable transport adapters. Key design decisions:

- **Adapter pattern** -- swap transports without changing application code. Use stdout for local development, HTTP for production, or build your own from the template.
- **Dispatch logic** -- route by tool name, capability, or custom matching rules.
- **Composable** -- the router works with or without the control layer. Without nexus-control, it routes unconditionally.

## Attestation layer: nexus-attest

Provides cryptographic signing and verification for tool outputs:

- **Signing** -- tool outputs are signed before leaving the system.
- **Verification** -- consumers verify that results came from the tool that claims them.
- **Independence** -- nexus-attest can operate standalone, without the router or control plane.

## Design principles

1. **Use what you need.** Each package is independently installable. You can use attestation without routing, routing without governance, or the full stack.
2. **Adapters are swappable.** The adapter pattern means transport is a pluggable concern, not a hardcoded dependency.
3. **Python native.** Standard `pip install -e .` workflow. No exotic build tools, no custom package managers.

[Back to landing page](/nexus-suite/)
