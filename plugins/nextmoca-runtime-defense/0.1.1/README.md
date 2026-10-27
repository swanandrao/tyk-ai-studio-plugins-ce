# Next Moca Runtime Defense for AI Agents

Next Moca is a request-side context control for agents routed through Tyk AI
Studio. At the `post_auth` hook, this plugin calls the hosted Next Moca service
and applies its delivery decision before the request reaches the configured LLM
provider.

The OCI image contains only the compiled Tyk plugin adapter. It does not embed
the Next Moca selection engine, security rules, a model, application context,
or customer credentials.

## What It Does

- Selects relevant eligible context while preserving provider message order,
  roles, tool identifiers, and non-content fields.
- Applies hosted `selected`, `fallback`, `sanitized_fallback`, and `blocked`
  delivery outcomes according to the configured mode.
- In `enforce`, returns HTTP 403 for a hosted security block and prevents the
  upstream provider request.
- Emits content-free receipts with outcome, reason, token counters, engine
  latency, selection ID, and any failure class.

It is not output moderation or tool-execution authorization.

## Install

Install the digest-pinned OCI artifact from AI Studio's Marketplace:

```text
oci://ghcr.io/nextmoca/tyk-ai-studio-runtime-defense-plugin@sha256:7e73616fcc6d33e3ad3d764fffcbff9f9d1490fbded3314abfea5ea16db2f032
```

Then:

1. Create a [Next Moca API key](https://docs.nextmoca.com/authentication#getting-an-api-key)
   and store it in Tyk's secret mechanism as `NEXTMOCA_API_KEY`.
2. Configure an explicit operating point and begin with `mode: shadow`.
3. Attach the plugin to the intended LLM/provider route and push the gateway
   configuration. Installing a plugin does not place it in traffic.
4. Inspect content-free receipts, then promote a measured canary to `active`
   or `enforce`.

The plugin supports OpenAI-compatible chat requests with string message
content. See the [plugin repository](https://github.com/nextmoca/tyk-ai-studio-runtime-defense)
for configuration, delivery modes, unsupported request handling, and failures.

## License

The plugin source is licensed under Apache-2.0. Next Moca and Needlepath names
and logos are trademarks of Next Moca; no trademark license is granted.
