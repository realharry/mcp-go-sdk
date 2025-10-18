# Examples

This folder contains small runnable examples demonstrating how to use the Go MCP SDK in different scenarios: clients, HTTP servers, and server transports and features. Each subdirectory contains a focused example; see subfolder READMEs for more details when available.

This top-level file collects a short description of each example so you can quickly find a sample that matches your use-case.

## Client examples

- `listfeatures/` — A small utility that connects to an MCP server (stdio or streamable HTTP) and lists all provided features (tools, resources, prompts). Useful for discovering what a server exposes.
- `loadtest/` — A simple load-testing client that repeatedly calls a specified tool on a streamable HTTP MCP server. Options allow you to configure concurrency, QPS, duration, and request timeouts.
- `middleware/` — Demonstrates how to add client-side middleware to modify outgoing requests (for example, injecting a progress token). This is a tiny example of adding request hooks to a `mcp.Client`.

## HTTP example

- `http/` — A combined server+client example showing how to run an MCP server over HTTP using the streamable transport and how a client can connect, list tools, and call a `cityTime` tool. See `examples/http/README.md` for usage and CLI examples.

## Server examples

The `server/` directory contains many small examples demonstrating server-side features and transports. Highlights:

- `hello/` — Minimal stdio server with a single `greet` tool. Good starting point for integrating MCP with CLI-style tools.
- `basic/` — In-memory transport example showing client/server interaction without network plumbing.
- `completion/` — Shows how to attach a custom CompletionHandler to an MCP server (used to provide completions for prompts or arguments).
- `everything/` — A large example that exercises most of the SDK: tools with structured/unstructured output, prompts, resources, logging, elicitations, sampling, and completions. Useful as a comprehensive reference.
- `memory/` — Demonstrates an example server that exposes a simple knowledge-base (create/read/search nodes, relations, observations) and optionally persists data to disk.
- `toolschemas/` — Shows various ways to declare tool input/output schemas: automatic schema derivation with helpers, manual schema handling, raw JSON schema usage, and custom schema tweaking.
- `sse/` — Demonstrates serving MCP over Server-Sent Events (SSE) HTTP endpoints. Exposes multiple greeter endpoints mapped by URL path.
- `distributed/` — Example of a parent process acting as a reverse proxy to multiple child MCP server processes (stateless child servers). Useful to understand patterns for scaling and proxying streamable MCP backends.
- `elicitation/` — Demonstrates elicitation: how a server can request structured data from a client (via an elicitation handler) and how the client can respond programmatically.
- `custom-transport/` — Shows how to implement a simple custom transport (newline-delimited JSON over stdin/stdout) and run a server with it. Useful as a template for building bespoke transports.
- `auth-middleware/` — Shows how to integrate authentication middleware (JWT, API keys, scope checks) with an MCP HTTP server. See `examples/server/auth-middleware/README.md` for details and usage.
- `rate-limiting/` — Example that demonstrates applying rate limiting to MCP endpoints (uses an HTTP streamable server and local rate-limiting logic).
- `middleware/` — Server-side middleware examples showing how to wrap handlers for logging, auth, or other cross-cutting concerns.
- `completion/` — (Also listed above) small example showing assignment of a CompletionHandler on server options.
- `sequentialthinking/` — Demonstrates an MCP server that implements sequential/stepwise thinking tools: start, continue, review thinking sessions with support for branching and revisions. See `examples/server/sequentialthinking/README.md` for full details.
- `toolschemas/` — (Also listed above) shows schema customization and manual validation examples.

## Running the examples

Most examples are small Go programs. Typical ways to run them:

1. Run directly with `go run` from the example directory, for example:

```bash
cd examples/http
go run . server
```

2. Many server examples accept command-line flags (see the `main.go` top comments or `-h` output). Several examples can be run in `server` or `client` mode where indicated.

If an example has its own README (for example `examples/http/README.md`, `examples/server/auth-middleware/README.md`, or `examples/server/sequentialthinking/README.md`), prefer those files for full usage instructions and deeper explanations.

## Notes

- Descriptions here are intentionally brief — they are meant to help you find relevant examples quickly. For detailed usage and configuration, open the example folder and read its README or `main.go`.
- If you want, I can expand any of these summaries into step-by-step run instructions or add small snippets showing the most important commands for each example.
