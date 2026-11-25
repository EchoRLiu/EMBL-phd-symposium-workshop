# Setup guide for AI-assisted coding

This repository contains information on the following:
- how to sign up to free academic LLM services (Blablador, de.NBI)
- how to set up the API with harnesses (OpenCode, Copilot) in VS Code
- how to set up a simple virtual machine with Multipass, and how to set up the API with harnesses (OpenCode, Copilot) in the created virtual machine.

> [!NOTE]
> These steps were tested on **macOS**, **Linux**, and **windows**. If something doesn't work for you, please [open an issue](../../issues).

## What you will set up

| Section | What |
|---|---|
| [0. Sign up and install](docs/0-sign-up-and-install.md) | Blablador and/or de.NBI accounts and API keys; VS Code, Git, GitHub, Multipass |
| [1. AI in VS Code](docs/1-ai-in-vscode.md) | Blablador and/or de.NBI in VS Code, with OpenCode or Copilot harnesses |
| [2. Sandboxing with Multipass](docs/2-sandboxing-with-multipass.md) | A coding agent inside an Ubuntu virtual machine |

## Security awareness

1. **Your API keys.** Enter them only through the tools' key prompts (e.g., `/connect`, VS Code's *Manage Language Models*). Never paste them into a chat, a prompt, your code or a file inside your project.
2. **On your laptop the agent has your permissions.** Choose the VM for anything the agent runs by itself.
3. **Keys stay on the laptop.** Clone, commit and push on your laptop; never put SSH keys or GitHub tokens inside the VM.
4. **Mount only the project folder**, never your home folder.
5. **Read the diff** (`git status`, `git diff`) before you commit anything the agent changed.

## Repository contents

```
docs/            step-by-step guides (start with 0-sign-up-and-install.md)
configs/         ready-to-copy config files, without any keys
  opencode/      OpenCode: Blablador and/or de.NBI
  vscode/        VS Code chat models: Blablador and/or de.NBI
  copilot-cli/   GitHub Copilot CLI: Blablador and/or de.NBI
```

## Acknowledgements

This guide has used [Blablador](https://helmholtz-blablador.fz-juelich.de), the LLM service of Helmholtz AI hosted by Forschungszentrum Jülich, and [de.NBI Cloud Bielefeld](https://llm.bi.denbi.de). We gratefully acknowledge **Blablador, the Helmholtz Association, Helmholtz AI, and de.NBI**.