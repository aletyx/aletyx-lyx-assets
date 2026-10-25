# Privacy

Aletyx Lyx is an internal tool for the Aletyx engineering team.

## What leaves your machine

| Data | Sent to | When |
|---|---|---|
| Your Claude API key | Anthropic (`api.anthropic.com`) | When you set the key (one call that lists models, to check it) and with each Ask Lyx request |
| Your Ask Lyx questions, the Home items you attach, and what Lyx's tools return (GitHub, Dev Dashboard, Jenkins, devLab, Maven and registry data, redacted) | Anthropic, under **your own** API key | When you send a question in Ask Lyx |
| Code from your editor | Anthropic, under your own API key | Only when you click **Attach file or selection** (or use **Ask Lyx About Selection**), and only the selection or file shown on the chip, at most 40,000 characters |
| OAuth tokens for the Dev Dashboard | Aletyx Dev Dashboard (`lyx.dashboardUrl`) | On sign-in, token refresh, sign-out and every MCP gateway call |
| A review request: the PR and the people you picked (and, if you chose it, marking a draft ready for review) | GitHub, with your own VS Code GitHub sign-in | Only when you click **Request** in the confirmation, or **Run** on Ask Lyx's card |
| Ship's GitHub actions: a new PR (its title and body as you edited them), a merge of your PR, deleting its branch | GitHub, with your own VS Code GitHub sign-in | Only when you click the confirmation on Ship's card (**Create PR**, **Merge**, **Delete branch**) |
| Ship's release run (the job and its parameters) | Aletyx Dev Dashboard, which asks Jenkins | Only when you click **Run release** on Ship's card |
| The folder, image and tag names you open (no credentials, no token) | Aletyx Maven (`maven.aletyx.services`) and registry (`registry.aletyx.services`), read anonymously | When you open Lyx Home's Maven or Registry tab, and as you browse it |

Data sent to Anthropic is governed by the terms of the Anthropic account that owns your API key. Lyx removes credentials (API keys, bearer tokens, JWTs, GitHub tokens, password and token fields) from text before logging it and before sending tool output to the model.

## What is stored locally

- The Claude API key and the Dev Dashboard tokens are stored only in VS Code SecretStorage (your OS keychain). They are never written to settings, logs or telemetry.
- The "Aletyx Lyx" output channel holds redacted logs.
- Ask Lyx conversations (your questions, attachments, the answers and what the tools returned) are kept in this workspace's VS Code storage on this machine, at most 50 conversations, unless `lyx.chat.keepHistory` is off. They are never sent to the Dev Dashboard. **Clear all** in Ask Lyx, or turning the setting off, deletes them.

## Telemetry

None. This version collects no telemetry. If telemetry is added later, it will respect VS Code's `telemetry.telemetryLevel` setting and will be listed here first.

## Server-side audit

Only people in the Dev Dashboard's admin and DevSecOps groups can run Jenkins jobs from Lyx (Home's Run a job, or a Run card in Ask Lyx), and an admin can turn a job off for Lyx; everyone else reads only. Every tool call made through the Lyx gateway is recorded by the Dev Dashboard (user, tool, redacted arguments, result status, time) as SOC 2 audit evidence.
