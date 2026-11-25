# Let the agent play — in a sandbox

Setup guide for the **EMBL PhD Symposium 2026 workshop** on AI-assisted coding: how to connect free academic LLM services (Blablador, de.NBI) to VS Code and to coding agents, and how to run those agents safely inside a virtual machine.

> [!NOTE]
> These steps were tested on **macOS** and **Linux**. The **Windows** steps follow the official documentation but have not been tested end to end yet. If something doesn't work for you, please [open an issue](../../issues).

## What you will set up

| Part | What | Where it runs |
|---|---|---|
| [0. Sign up and install](docs/0-sign-up-and-install.md) | Blablador and/or de.NBI accounts and API keys; VS Code, Git, GitHub, Multipass | Your laptop |
| [1. AI in VS Code](docs/1-ai-in-vscode.md) | An AI model in your editor, with OpenCode or VS Code's own chat | Your laptop (**no sandbox**) |
| [2. Sandboxing with Multipass](docs/2-sandboxing-with-multipass.md) | A coding agent inside an Ubuntu virtual machine | A VM on your laptop |
| [Security checklist](docs/security-checklist.md) | What to check before, during and after | Everywhere |

## Which setup should I use?

| Your laptop | Part 1: in VS Code | Part 2: inside the VM |
|---|---|---|
| macOS or Linux | OpenCode + Blablador | OpenCode + Blablador |
| Windows | VS Code chat (Local or Copilot harness) + Blablador | OpenCode + Blablador |

Inside the VM everyone uses Ubuntu, so Part 2 is the same on every laptop. Only the few commands you type on your laptop (copying or mounting files) differ, and both versions are shown.

**Blablador** is the easier service to sign up for and works best with these tools. **de.NBI** is optional; you need a Life Science Login linked to a German research institution.

## Do these before the workshop

Some steps involve waiting for emails or downloads:

- [ ] Sign up for Blablador and create your API key (the confirmation email can take a few minutes)
- [ ] Optional: sign up for de.NBI (approval can take 20 minutes or more)
- [ ] Install VS Code, Git and Multipass (version 1.17.2 or newer)
- [ ] Launch one throwaway VM so the Ubuntu image is already downloaded, then delete it:
      `multipass launch --name warmup` and afterwards `multipass delete --purge warmup`

## Security in one minute

1. **Your API keys are passwords.** Enter them only through the tools' key prompts (`/connect`, VS Code's *Manage Language Models*, `read -rs`). Never paste them into a chat, a prompt, your code or a file inside your project.
2. **On your laptop the agent has your permissions.** Prefer the VM for anything the agent runs by itself.
3. **Keys stay on the laptop.** Clone, commit and push on your laptop; never put SSH keys or GitHub tokens inside the VM.
4. **Mount only the project folder**, never your home folder.
5. **Read the diff** (`git status`, `git diff`) before you commit anything the agent changed.

More in the [security checklist](docs/security-checklist.md).

## Repository contents

```
docs/            step-by-step guides (start with 0-sign-up-and-install.md)
configs/         ready-to-copy config files, without any keys
  opencode/      OpenCode: Blablador + de.NBI
  vscode/        VS Code chat models: Blablador + de.NBI
  copilot-cli/   GitHub Copilot CLI: Blablador + de.NBI
```

## Acknowledgements

This workshop uses [Blablador](https://helmholtz-blablador.fz-juelich.de), the LLM service of Helmholtz AI hosted by Forschungszentrum Jülich. We gratefully acknowledge **Blablador, the Helmholtz Association and Helmholtz AI**.

We also thank the [de.NBI Cloud Bielefeld](https://llm.bi.denbi.de) for access to its LLM API.

The sandboxing part builds on the course material *Responsible Use of Generative AI in Assisted Coding*, Scenario III: Full Agentic Code Development.
