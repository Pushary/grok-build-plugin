# Security

## Reporting a vulnerability

Email **security@pushary.com** with details and reproduction steps. Please do not open a public
issue for security reports. We aim to acknowledge within 72 hours.

## What this plugin contains

Two files that change behavior: `.mcp.json`, which points Grok Build at the Pushary MCP server at
`https://pushary.com/api/mcp/mcp`, and `skills/pushary/SKILL.md`, which is text guidance for the
agent. There are no hooks, commands, agents, scripts or dependencies, and no credential is
committed to this repository. The plugin itself downloads and runs nothing.

## How it signs in

The server is declared as a remote HTTP MCP server with no headers. You sign in with your Pushary
account over OAuth in your browser; the authorization server is `https://clerk.pushary.com`. Grok
Build registers itself as an OAuth client during sign-in and keeps the token in
`~/.grok/mcp_credentials.json`.

A signed-in connection can call six tools: `ask_user`, `wait_for_answer`, `cancel_question`,
`propose_scope`, `send_notification` and `schedule_reminder`. It cannot read or change policies,
subscribers, campaigns or API keys.

## What Grok Build sends

Only the arguments of the Pushary tool calls it makes: question and notification text, optional
context such as a summary or an error message, an agent name and a session id. A question that
approves a tool call also carries the command or the diff of an edit, up to 4,000 characters, and
the server removes secrets it recognises from it before storing it.

## Optional hooks are not part of this plugin

The README describes `npx pushary@latest setup --agents grok`, which installs Pushary's tool-call
hooks for phone approvals. The plugin does not run it. When the Pushary tools are not connected, the
skill's setup section can have the agent inspect the machine (`uname`; whether a Pushary key is set
in the environment or stored in `~/.pushary/config.json`, without printing it; whether Node, npm
and the Mac app are installed), check and repair an existing install (`npx pushary@latest status`, then
`setup` or `pair` if status says to, or the Mac app when Node is missing), or
offer to install Pushary: the Mac app with `brew install --cask pushary/tap/pushary`, or the command
line with `npx pushary@latest setup`, followed by `pair` or `doctor` when needed. The agent runs them
as ordinary shell commands, under Grok Build's permission mode, and the skill tells it to explain
what setup does before running it.
