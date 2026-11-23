<p align="center">
  <img src="assets/logo.png" alt="Pushary" width="72" height="72" />
</p>

<h1 align="center">Pushary for Grok Build</h1>

<p align="center">When Grok Build needs a decision, Pushary sends the question to your phone. Miss the push with calls enabled and Pushary can ring you. Give your answer and Grok Build continues in the same session.</p>

---

## What it does

Grok Build keeps working after you walk away from the terminal. Pushary reaches you on your phone or Mac, in the same inbox as your other AI agents such as Claude Code, Codex and Cursor.

1. **Ask.** When Grok needs a decision only you can make, it asks you through Pushary: yes or no, a choice of options, or a short answer. You answer from the Pushary phone or Mac app, and Grok carries on.
2. **Notify.** When a long task finishes, or fails in a way Grok cannot fix, Grok sends you a push with the result.
3. **Remind.** Grok can set a one-time personal reminder that Pushary delivers later.

The bundled `pushary` skill tells Grok when to reach you and when to stay quiet: it asks only for decisions it cannot make itself, folds several into one question, and sends at most three pushes per task, unless you ask for more or it needs an approval to carry on.

## What you get after you sign in

1. Sign in and pick a plan. New customers start with a 3-day trial.
2. Install this plugin and sign in from `/mcps` with the same account. For approvals before a command runs, also run `npx -y pushary@latest setup --agents grok` once.
3. When Grok needs a yes or an answer, the question arrives on your phone (the Pushary app for iOS and Android), on your Mac, or in the dashboard.
4. You answer with one tap, or type a short reply, and Grok carries on. The dashboard keeps a record of what each agent asked and what you answered.

See [Grok Build notifications and phone approvals](https://pushary.com/grok-build-notifications?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme).

## Plans

Each plan starts with a 3-day trial for new customers. During the trial, Agent, Agent Pro and Team include 5 call minutes.

| Plan | Price | What you get |
| --- | --- | --- |
| [Agent](https://pushary.com/pricing?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) | $9.99 a month | One person and every AI agent they run. Approve, deny or answer from your phone or Mac. 10 call minutes a month. |
| [Agent Pro](https://pushary.com/pricing?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) | $19.99 a month | Everything in Agent, plus unlimited notifications, budgets and priority support. 20 call minutes a month. |
| [Team](https://pushary.com/teams?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) | $59 a month for 5 people, $12 for each extra person | Each person gets their own agent’s questions. On supported hooks, route a step such as a production deploy to the teammate who approves it. See who answered in the shared record. Includes export and 60 shared call minutes a month. |

Missed the push? Pushary can call you, by default after 1 minute, and read the request. You approve it, say no or tell the agent what to do. Calls need a confirmed phone number and work in English, German, French and Dutch. [Phone calls](https://pushary.com/calls?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) · [Calls for Grok Build](https://pushary.com/grok-build-phone-call?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) · [How calls work](https://pushary.com/docs/agents/phone-calls?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme)

## What is in this plugin

| Component | File | What it does |
| --- | --- | --- |
| MCP server | `.mcp.json` | Connects Grok Build to Pushary's hosted MCP server at `https://pushary.com/api/mcp/mcp` |
| Skill | `skills/pushary/SKILL.md` | Instructions for when to ask, when to notify and how to wait for an answer |

The plugin adds no hooks, commands, agents, scripts or dependencies. When the Pushary tools are not connected, the skill's setup section can have Grok look for an existing Pushary install (whether a Pushary key is set or stored, without printing it, whether Node and npm are installed, and whether the Mac app is), check and repair one it finds (`npx -y pushary@latest status`, then `setup` or `pair` if status says to, or the Mac app when Node is missing), or offer to install Pushary: the Mac app with `brew install --cask pushary/tap/pushary`, or the command line with `npx -y pushary@latest setup`, followed by `pair` or `doctor` when needed. Grok runs these like any other command, under your permission mode, and the skill tells it to explain setup before running it.

## What connecting does

Before you sign in, know what is shared.

- **Network endpoints.** Grok Build calls `https://pushary.com/api/mcp/mcp` for the Pushary tools, and `https://clerk.pushary.com` once, to sign you in.
- **Credentials.** You sign in with your Pushary account over OAuth in your browser. There is no API key to paste. Grok Build registers itself with Pushary during sign-in and stores the token in `~/.grok/mcp_credentials.json`.
- **What Grok sends.** Only what it puts in a Pushary tool call: the question or notification text, optional detail such as a summary or an error message, the agent name and a session id. A question that approves a tool call also carries what it approves: the command, or the diff of an edit, up to 4,000 characters. Pushary removes secrets it recognises from it before storing it. Pushary stores these so they show in your inbox and history.
- **What Pushary does not see.** Your Grok sessions, your files and your other tools, apart from what Grok puts in a tool call.
- **What the connection can do.** Ask questions, read and cancel them, propose a task boundary for you to approve, send notifications and schedule reminders. It cannot read or change your Pushary policies, subscribers, campaigns or API keys.

Read the [privacy policy](https://pushary.com/privacy) for retention details.

## What you need

- A paid Pushary plan for your own agents, such as Agent, Agent Pro or Team. Eligible web sign-ups get a trial; see [pricing](https://pushary.com/pricing?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme).
- The Pushary app on your phone, or the Pushary Mac app, signed in to the same account. Get them at [pushary.com/download](https://pushary.com/download).

## Install

From GitHub:

```bash
grok plugin install Pushary/grok-build-plugin
```

Start Grok Build, run `/mcps`, select **pushary** and press `i` to sign in. Sign in with your Pushary account in the browser and allow access.

Sign in once in the interactive app. Headless runs such as `grok -p` cannot open a browser, so they skip a server that has no stored sign-in, and use the one you stored here.

Then check that a question reaches you. Ask Grok:

```text
Use Pushary to ask me "Did this reach you?" as a yes or no question, with agentName "Grok Build - Setup check". Wait for my answer and tell me what I chose.
```

Answer on your phone. Grok should tell you your answer.

## Approve tool calls from your phone

This plugin lets Grok ask you. It does not stop Grok from running a command. To approve shell commands, edits and MCP calls from your phone before they run, install Pushary's hooks with the Pushary command line:

```bash
npx -y pushary@latest setup --agents grok
```

Setup pairs your phone, writes Grok Build hooks to `~/.grok/hooks/pushary.json`, and adds its own `pushary` MCP server with an agent key to `~/.grok/config.toml`. Grok Build then uses that server in place of the one in this plugin, and questions it asks stay open until you answer them. Read the [Grok Build guide](https://pushary.com/docs/agents/guides/grok-build?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme) before you run it.

## What it does not do

- It does not gate Grok's tool calls on its own. Grok's permission modes and allow and deny rules still decide what runs. Use the hooks above for phone approvals.
- A question asked through this sign-in closes 10 minutes after it is sent. A question that closes unanswered is never treated as a yes.
- Grok decides when to call Pushary. The skill guides it; nothing forces it.

## Support

- Guide: [pushary.com/docs/agents/guides/grok-build](https://pushary.com/docs/agents/guides/grok-build?utm_source=github&utm_medium=oss-adapter&utm_campaign=grok-build-plugin&utm_content=readme)
- Help: [pushary.com/support](https://pushary.com/support)
- Security reports: see [SECURITY.md](SECURITY.md)

## Related repositories

- [Pushary for Grok Bot](https://github.com/Pushary/grok-bot-plugin): the connector for Bots that run on Grok's cloud computer.
- [Pushary skill](https://github.com/Pushary/pushary-skill): the skill, and `npx -y pushary@latest setup` for approval hooks in Grok Build, Claude Code, Codex and more.
- [Pushary for Mac](https://github.com/Pushary/pushary-mac): answer from the notch on your Mac.

## License

MIT. See [LICENSE](LICENSE).
