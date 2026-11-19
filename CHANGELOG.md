# Changelog

## 0.1.1

- `pushary` skill 0.13.5, from 0.13.4: on a `select` question, agents pass `allowOther: true` unless their options cover every answer, so you can type your own reply instead of picking the closest option. The Other box shows on the pushary.com decision page and in the Android app from 1.0.64; the iOS app gets it with 1.0.65. Other places you answer show the options as before.

## 0.1.0

- First release. Grok Build connects to Pushary's hosted MCP server with a Pushary sign-in, and the bundled `pushary` skill tells it when to ask you a question on your phone and when to send a push.
