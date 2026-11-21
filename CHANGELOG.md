# Changelog

## 0.1.2

- `pushary` skill 0.13.6, from 0.13.5: a risky step, such as a recursive delete, a force-push or a deploy, is no longer described as deny-only on the phone. The Pushary app approves one from 1.0.66 after Face ID or the phone's passcode. The lock screen, an older app and a workspace that requires the keyboard for risky steps still offer only deny and `defer` ("Handle on your machine"). What an agent passes and how it reads `defer` are unchanged.

## 0.1.1

- `pushary` skill 0.13.5, from 0.13.4: on a `select` question, agents pass `allowOther: true` unless their options cover every answer, so you can type your own reply instead of picking the closest option. The Other box shows on the pushary.com decision page and in the Android app from 1.0.64; the iOS app gets it with 1.0.65. Other places you answer show the options as before.

## 0.1.0

- First release. Grok Build connects to Pushary's hosted MCP server with a Pushary sign-in, and the bundled `pushary` skill tells it when to ask you a question on your phone and when to send a push.
