# Klisten AgentEscrow for Gemini CLI — v0.1.0

Read an existing private unfunded draft from your organization.

Inspect stated draft terms by UUID. Successful results remain UNFUNDED_DRAFT, funds=unfunded and release_authorized=false. This connector neither creates drafts nor holds money, funds transactions, pays, verifies delivery or resolves disputes.

## What you need

Use your own dedicated Klisten API key with `escrow:read`. Sign in at https://klisten.co.kr/app. Store the key only in the sensitive extension setting `KLISTEN_AGENTESCROW_API_KEY`. Never put it in a prompt, tool arguments, source code or public repository. No shared operator credentials or OAuth client are included.

Needs an existing same-organization unfunded draft UUID; no shared private record or credentials supplied.

Endpoint: https://api.klisten.co.kr/mcp/agentescrow
Tools: `agentescrow_draft_get`.

## Install and configure

Install the published source with `gemini extensions install https://github.com/daehoonkwon-hash/klisten-agentescrow-gemini-extension`. If using a downloaded copy, the local alternative is `gemini extensions install ./klisten-agentescrow`. Supply the key through the sensitive setting when prompted.

Gemini CLI 0.63 redacts API_KEY environment values in MCP headers by default. Merge `GEMINI_SETTINGS_FRAGMENT.json` into your chosen isolated Gemini profile settings.json, retaining existing settings. It explicitly allows ONLY `KLISTEN_AGENTESCROW_API_KEY`. It contains the variable name, not a secret. Never disable environment redaction globally or allow all variables. Without the narrow exception, the credential is not transmitted correctly.

Inspect `/mcp` after configuration. Tool discovery by itself does not establish authorization: first perform an appropriate safe call against your own eligible data. Do not invent record IDs or treat missing records as a successful demo.

## Examples and expected results

- Read my existing draft UUID. Tools: agentescrow_draft_get. Expected: Authorized unfunded draft.
- Summarize that draft while checking whether funds are held. Tools: agentescrow_draft_get. Expected: Explicitly unfunded, no release authorization.
- Try a nonexistent or foreign-organization draft. Tools: agentescrow_draft_get. Expected: Safe unavailable/denied result.

## Scope and charges

The extension package itself is an integration, not a payment or service guarantee. Existing service prerequisites and pricing apply. Installing never replenishes credit or authorizes a paid scan. Do not perform a monetary transfer or paid operation for a smoke test. Data creation, license acceptance and deletion require the account holder's authorization. There is no model execution within this MCP adapter.

## Verified evidence and limits

On 2026-10-13, local installation/list/removal checks passed using an isolated Gemini CLI 0.63 profile. A separate scripted harness then used the actual Gemini native MCP transport, tool discovery and DiscoveredMCPTool invocation against the existing HTTPS service. Existing own-organization draft returned UNFUNDED_DRAFT, funds=unfunded and release_authorized=false. No draft was created or money transferred.

Local invalid-input validation rejected the empty request. The native wrong-scope call returned a tool error but did not expose a typed authentication code, so that native classification remains unverified. A separate request to the corresponding production REST route returned HTTP 403 / INSUFFICIENT_SCOPE. The separate REST request reused the same valid fixture with a wrong-scope key. This is direct REST evidence and must not be presented as an interactive Gemini conversation.

Interactive Gemini model conversation: NOT_VERIFIED. Public gallery listing: NOT_VERIFIED. These checks do not promise zero defects, uptime, safety certification or future performance. Trial keys and parent-created fixtures are temporary, not shared customer access.

## Removal and data handling

Run `gemini extensions uninstall klisten-agentescrow`. Uninstalling does not revoke an API key or delete hosted records. Revoke the dedicated key separately when it is no longer needed. Never expose private records or customer identifiers in public demos.

Documentation: https://klisten.co.kr/docs.html
Privacy: https://klisten.co.kr/privacy.html
Terms: https://klisten.co.kr/terms.html
Support: klisteninc@gmail.com
