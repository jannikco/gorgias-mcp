# Gorgias MCP server

Find existing customers and explicitly create one customer record with an email channel.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `GORGIAS_EMAIL`
- `GORGIAS_API_KEY`
- `GORGIAS_SUBDOMAIN`



Credential help: https://dash.readme.com/api/v1/api-registry/209muffmufcb2cu

## Provider setup

Use your Gorgias account email as the Basic username and your personal API key as password. GORGIAS_SUBDOMAIN is the account label. Contact data and any downstream automations remain subject to your account permissions.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call gorgias_list_customers '{"limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/gorgias-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| gorgias_list_customers | Read | List a bounded page of support customers. |
| gorgias_create_customer | Explicit approval required | Create a customer with explicit contact channels; no message is sent. |

## Concrete workflow

Find existing customers and explicitly create one customer record with an email channel.

1. gorgias_list_customers
2. gorgias_create_customer

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=gorgias&integration=gorgias-mcp&utm_source=github&utm_campaign=github-gorgias-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/gorgias/).

## Provenance and maintenance

- https://dash.readme.com/api/v1/api-registry/209muffmufcb2cu

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
