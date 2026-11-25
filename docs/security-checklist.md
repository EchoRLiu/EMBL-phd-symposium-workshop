# Security checklist

[← Back to overview](../README.md)

## API keys

- [ ] **Blablador key:** a legacy token with **only** the `read_user` scope, and an expiry date. It's a token for your Helmholtz GitLab account, so never give it `api` or `write_*` scopes.
- [ ] Enter keys only through the tools' key prompts: `/connect` or `opencode auth login` in OpenCode, **Chat: Manage Language Models** in VS Code, `read -rsp` in the terminal.
- [ ] Never paste a key into an AI chat or prompt, into your code, or into any file inside your project folder. Our [`.gitignore`](../.gitignore) blocks the usual file names, but don't rely on it.
- [ ] Never share your key with other people.
- [ ] Know where each tool keeps your key:

  | Tool | Where the key is stored |
  |---|---|
  | VS Code chat | Your system's secure storage (only a reference is in `chatLanguageModels.json`) |
  | OpenCode | `~/.local/share/opencode/auth.json`, plain text, readable only by your user |
  | Copilot CLI, quick setup | An environment variable that disappears when you close the shell |
  | Copilot CLI, `providers.json` | Plain text in `~/.copilot/providers.json`: use only in the VM, and run `chmod 600` on it |

- [ ] Inside the VM, the agent can read every key stored there. Use keys you can revoke, and revoke them when you no longer need them.

## On your laptop (no sandbox)

- [ ] OpenCode lets the agent run commands, edit files and access folders outside your project **without asking**, unless you configure otherwise. Use our [`opencode.json`](../configs/opencode/opencode.json), which asks first.
- [ ] In VS Code's agent mode, keep the approval of terminal commands on; don't turn on auto-approve.
- [ ] Anything the agent should do by itself belongs in the VM.

## In the VM

- [ ] Clone, commit and push **on your laptop**. No SSH keys, GitHub tokens or other credentials in the VM.
- [ ] Mount **only your project folder**, never your home folder.
- [ ] Windows: mounts run with administrator rights. Turn them off when you're done: `multipass set local.privileged-mounts=false`.
- [ ] Take a snapshot before big tasks, and delete the VM when you're finished.

## Before you keep the agent's changes

- [ ] `git status` and `git diff`: read every change.
- [ ] `.git/hooks` should contain only `*.sample` files. Hooks run on your laptop when you commit, and `git diff` doesn't show them.
- [ ] Check new install scripts, new dependencies (`requirements.txt`, `package.json`, …) and new `.vscode/` settings. AIs sometimes invent package names, and attackers register them ("slopsquatting").
- [ ] When VS Code asks whether you trust the authors of a folder the agent changed, choose **No** until you've reviewed it.
- [ ] Try new code inside the VM first.

## Plugins and extensions

- [ ] Plugins (like `opencode-blablador`) and VS Code extensions run with your permissions. Install them from the official sources, and pin plugin versions as our configs do.

## Data

- [ ] Don't send personal, patient or unpublished confidential data to any hosted model, even a zero-retention one.
