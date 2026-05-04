# MCP Server & SDK

OmniFlow provides three programmatic interfaces for agent integration: a REST API, language SDKs (TypeScript and Python), and a native MCP (Model Context Protocol) server. This page describes the interfaces and provides links to detailed reference documentation.

## REST API

The OmniFlow REST API exposes the protocol's investor-facing functionality as standard HTTP endpoints. Core endpoints:

- GET /api/v1/products — List available products with metadata

- GET /api/v1/products/{id} — Product detail including full risk metrics

- GET /api/v1/risk-oracle/{assetId} — Current and historical risk metrics

- GET /api/v1/nav/{assetId} — Current and historical NAV

- POST /api/v1/subscribe — Submit a subscription (requires authenticated principal)

- POST /api/v1/redeem — Submit a redemption request

- GET /api/v1/positions — Current positions for the authenticated principal

- GET /api/v1/distributions — Distribution history and pending claims

- POST /api/v1/distributions/claim — Claim available distributions

Authentication is via API key bound to the verified Principal. All write operations additionally require an EIP-712 signed authorization from the Principal's designated signer or a delegated agent within scope.

Full API reference is available at api.omniflow.xyz/docs.

## TypeScript SDK

The TypeScript SDK is the recommended interface for Node.js-based agent runtimes and web applications.

typescript

import { OmniFlow } from '@omniflow/sdk';

const client = new OmniFlow({

apiKey: process.env.OMNIFLOW_API_KEY,

signer: agentSigner, // ethers.js Signer with delegated authority

});

// List products

const products = await client.products.list({ tier: 1 });

// Get risk metrics

const risk = await client.risk.get(products[0].assetId);

// Submit subscription (requires principal grant)

const subscription = await client.subscribe({

productId: products[0].id,

amount: '100000', // USDC

currency: 'USDC',

});

The SDK handles transaction signing, nonce management, and retry logic. Source code is available at github.com/omniflow/sdk-typescript under the Apache 2.0 license.

## Python SDK

The Python SDK provides equivalent functionality for Python-based agent runtimes.

python

from omniflow import OmniFlow

client = OmniFlow(

api_key=os.environ['OMNIFLOW_API_KEY'],

signer=agent_signer, # web3.py LocalAccount with delegated authority

)

# List products

products = client.products.list(tier=1)

# Get risk metrics

risk = client.risk.get(products[0].asset_id)

# Submit subscription

subscription = client.subscribe(

product_id=products[0].id,

amount='100000',

currency='USDC',

)

Source code is available at github.com/omniflow/sdk-python under the Apache 2.0 license.

## MCP Server

The OmniFlow MCP Server exposes protocol functionality as tools callable by LLM-based agents using Anthropic's Model Context Protocol. The server runs as a standalone service that LLM clients (Claude, GPT, custom runtimes) can connect to.

**Available tools:**

- list_products — Browse available investment products

- get_product_details — Detailed product information including risk metrics

- check_eligibility — Verify the connected agent's eligibility for a product

- simulate_subscription — Simulate a subscription without execution (sandbox)

- submit_subscription — Execute a subscription (subject to permission scope)

- get_positions — Retrieve current positions

- claim_distributions — Claim available distributions

- get_risk_metrics — Retrieve standardized risk metrics

**Connection:**

mcp connect https://mcp.omniflow.xyz \

--principal <principal-id> \

--agent <agent-id>

The MCP server enforces all KYA permissions. An agent connected to the MCP server cannot execute actions outside its delegated scope, regardless of LLM instructions.

Full MCP server reference is available at docs.omniflow.xyz/mcp.

## Sandbox Environment

A sandbox environment is provided for agent development and testing. The sandbox replicates the production protocol with synthetic assets, simulated NAV updates, and no real capital. Sandbox endpoints:

- REST API: https://api-sandbox.omniflow.xyz

- MCP: mcp connect https://mcp-sandbox.omniflow.xyz

Sandbox accounts are provisioned on request. Contact engineering@omniflow.xyz to obtain sandbox credentials.

## Versioning and Deprecation

OmniFlow follows semantic versioning for all programmatic interfaces. Breaking changes are introduced only at major version boundaries with at least 6 months of overlap support for the previous major version. Deprecations are announced through:

- The OmniFlow developer mailing list

- The protocol's GitHub release notes

- API response headers (X-OmniFlow-Deprecation for soon-to-deprecate endpoints)

## Open Source Components

The TypeScript SDK, Python SDK, and reference smart contract interfaces are released under the Apache 2.0 license. The MCP server is closed-source but provides a documented protocol that third parties may implement against.
