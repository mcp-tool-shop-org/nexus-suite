---
title: Reference
description: CLI usage, configuration, and adapter API reference.
sidebar:
  order: 4
---

## CLI usage

### nexus-router

```bash
nexus-router --adapter <adapter-name> [options]
```

| Flag | Description |
|------|-------------|
| `--adapter` | Transport adapter to use (`stdout`, `http`, or a custom adapter name) |

### Running tests

Each package uses pytest:

```bash
cd src/<package-name>
pytest
```

## Configuration

### nexus-control policies

nexus-control reads governance policies from its configuration. Policies define:

| Policy type | Purpose |
|-------------|---------|
| Access rules | Which tools can be invoked and by which callers |
| Rate limits | Request throttling per tool or per caller |
| Audit settings | What gets logged and where audit trails are stored |

### Adapter configuration

Each adapter may accept its own configuration. The stdout adapter requires no configuration. The HTTP adapter accepts endpoint URLs and authentication settings specific to your deployment.

## Adapter API surface

Custom adapters implement the adapter interface expected by nexus-router. At minimum, an adapter must:

1. **Accept a dispatch request** -- receive the tool name, input payload, and routing metadata.
2. **Deliver the request** -- transport the payload to the target tool using the adapter's transport mechanism.
3. **Return the response** -- pass the tool output back to the router.

Use `nexus-router-adapter-template` as a starting point. It provides the required interface with placeholder implementations.

## Attestation API

### Signing

nexus-attest signs tool outputs before they leave the system. The signing process attaches a cryptographic signature to the output payload.

### Verification

Consumers call the verification API to confirm that a result was produced by the claimed tool. Verification checks the signature against the expected signing identity.

## Architecture layers summary

| Layer | Package | Responsibility |
|-------|---------|---------------|
| Control | nexus-control | Governance policies, configuration, access rules, rate limits |
| Routing | nexus-router | Request dispatch to tools via pluggable transport adapters |
| Attestation | nexus-attest | Cryptographic signing and verification of tool outputs |

## Links

- [GitHub repository](https://github.com/mcp-tool-shop-org/nexus-suite)
- [nexus-router standalone](https://github.com/mcp-tool-shop-org/nexus-router)
- [nexus-attest standalone](https://github.com/mcp-tool-shop-org/nexus-attest)
- [MCP Tool Shop org](https://github.com/mcp-tool-shop-org)

[Back to landing page](/nexus-suite/)
