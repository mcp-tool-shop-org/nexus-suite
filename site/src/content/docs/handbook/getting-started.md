---
title: Getting Started
description: Install Nexus Suite components and run your first test.
sidebar:
  order: 1
---

## Prerequisites

- Python 3.10 or later
- pip (included with Python)
- Git

## Clone the repository

```bash
git clone https://github.com/mcp-tool-shop-org/nexus-suite.git
cd nexus-suite
```

## Install a component

Each package lives under `src/` and can be installed independently. For example, to install the router:

```bash
cd src/nexus-router
pip install -e .
```

Repeat for any other component you need:

```bash
# Attestation
cd src/nexus-attest
pip install -e .

# Governance control plane
cd src/nexus-control
pip install -e .
```

## Install an adapter

Router adapters are also independent packages:

```bash
# stdout adapter (local dev / CLI)
cd src/nexus-router-adapter-stdout
pip install -e .

# HTTP adapter (production)
cd src/nexus-router-adapter-http
pip install -e .
```

## Run tests

From any component directory:

```bash
pytest
```

Or run the full suite from the repo root if a top-level test runner is configured.

## Next steps

- Read the [Architecture](/nexus-suite/handbook/architecture/) guide to understand how the layers fit together.
- Explore individual [Projects](/nexus-suite/handbook/projects/) for package-specific details.

[Back to landing page](/nexus-suite/)
