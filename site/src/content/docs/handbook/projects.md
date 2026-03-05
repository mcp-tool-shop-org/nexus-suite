---
title: Projects
description: Overview of all six packages in the Nexus Suite monorepo.
sidebar:
  order: 3
---

Nexus Suite is a monorepo containing six independent Python packages. Each lives under `src/` and can be installed and used on its own.

## Core packages

### nexus-router

Request routing and dispatch. The central coordinator that receives incoming requests and sends them to the right tool through a transport adapter.

```bash
cd src/nexus-router
pip install -e .
```

- Pluggable adapter system for different transports
- Route by tool name, capability, or custom rules
- Works with or without nexus-control

### nexus-attest

Attestation signing and verification. Provides cryptographic proof that tool outputs came from the claimed source.

```bash
cd src/nexus-attest
pip install -e .
```

- Sign tool outputs before they leave the system
- Verify signatures on received results
- Fully independent -- no dependency on other Nexus packages

### nexus-control

Governance policy control plane. Defines and enforces access rules, rate limits, and audit trails.

```bash
cd src/nexus-control
pip install -e .
```

- Centralized policy configuration
- Access control and rate limiting
- Audit trail logging

## Router adapters

Adapters implement the transport layer for nexus-router. Swap them without changing application code.

### nexus-router-adapter-stdout

Debug and local development adapter. Routes tool output to stdout for inspection.

```bash
cd src/nexus-router-adapter-stdout
pip install -e .
```

Best for: local development, CLI tools, piped workflows.

### nexus-router-adapter-http

Production adapter for HTTP/REST dispatch.

```bash
cd src/nexus-router-adapter-http
pip install -e .
```

Best for: production deployments, remote tool invocation.

### nexus-router-adapter-template

Starter template for building custom transport adapters. Clone this when you need a transport that does not exist yet.

```bash
cd src/nexus-router-adapter-template
pip install -e .
```

Best for: custom integrations, proprietary transports.

## Package independence

Every package has its own `setup.py` or `pyproject.toml`, its own test suite, and zero mandatory cross-dependencies within the monorepo. You can install `nexus-attest` without ever touching `nexus-router`.

[Back to landing page](/nexus-suite/)
