# 1. AI in VS Code

[← 0. Sign up and install](0-sign-up-and-install.md) · Next: [2. Sandboxing with Multipass →](2-sandboxing-with-multipass.md)

Two ways to use Blablador or de.NBI from VS Code on your laptop:

| | [Option A: OpenCode](#option-a-opencode) | [Option B: VS Code's own chat](#option-b-vs-codes-own-chat-with-your-key) |
|---|---|---|
| Recommended for | macOS, Linux | Windows |
| What it is | A coding agent in the terminal, plus an optional VS Code extension | VS Code's chat with your own API key (*bring your own key*) |

> [!WARNING]
> Everything on this page runs **directly on your laptop, without a sandbox**. An agent here can do anything your user account can do. Keep the permission prompts on, and use [the VM (Part 2)](2-sandboxing-with-multipass.md) for anything the agent should do by itself.

---

## Option A: OpenCode

### A1. Install OpenCode

Go to <https://opencode.ai/>, choose the **Terminal** install option (not the desktop app download) and copy the command shown there.

- **macOS and Linux:** Homebrew is recommended. Without Homebrew, use the `curl` command, which works out of the box on macOS and Linux. At the time of writing it is:
  ```bash
  curl -fsSL https://opencode.ai/v2/install | bash
  ```
- **Windows:** Windows package managers (Scoop, Chocolatey) aren't supported. Install Node.js first, then use the **npm** command from opencode.ai:
  1. Download the **LTS Windows Installer (.msi)** from <https://nodejs.org/>.
  2. Run it and accept the license agreement.
  3. Keep the default installation path, and make sure **Add to PATH** and **npm package manager** are enabled.
  4. Click **Install** and finish the wizard, then open a new terminal and run the npm command from opencode.ai.

Then check that it works. You should see version 2.x:

```bash
opencode --version
```

Optional: install the **OpenCode** extension from the VS Code Extensions view.

### A2. Add the configuration

We provide a ready-made OpenCode configuration in [`configs/opencode/`](../configs/opencode/):

| File | Use it when |
|---|---|
| [`opencode.json`](../configs/opencode/opencode.json) | **Recommended on your laptop.** Blablador via the `opencode-blablador` plugin, de.NBI, and the agent asks before running commands or editing files |
| [`opencode.no-plugin.json`](../configs/opencode/opencode.no-plugin.json) | Same, but with Blablador set up by hand instead of through the community plugin |
| [`opencode.vm.json`](../configs/opencode/opencode.vm.json) | Inside the VM (Part 2): the agent works without asking |

OpenCode reads its global configuration from:

- macOS and Linux: `~/.config/opencode/opencode.json`
- Windows: `%USERPROFILE%\.config\opencode\opencode.json`

If you don't have that file yet, copy ours there. Run this from the folder where you cloned this repository:

```bash
# macOS and Linux
mkdir -p ~/.config/opencode
cp configs/opencode/opencode.json ~/.config/opencode/opencode.json
```

```powershell
# Windows (PowerShell)
New-Item -ItemType Directory -Force "$HOME\.config\opencode" | Out-Null
Copy-Item configs\opencode\opencode.json "$HOME\.config\opencode\opencode.json"
```

If you already have an `opencode.json`, don't overwrite it: copy the parts you need into it by hand.

Then install the Blablador plugin:

```bash
opencode plugin add opencode-blablador@0.1.5
```

> [!NOTE]
> `opencode-blablador` is a community plugin and runs with your permissions. We pin a tested version (`@0.1.5`). If you'd rather not use it, take `opencode.no-plugin.json` instead and skip this command.

### A3. Add your API key

Never paste your key into the chat or into the config file. Instead:

1. Start OpenCode by typing `opencode`.
2. Type `/connect`.
3. Search for **Blablador** (or **denbi**). It appears because of the plugin or the config file.
4. Paste your API key.

Or, from a normal terminal (not inside OpenCode):

```bash
opencode auth login blablador --method key
opencode auth login denbi --method key
```

OpenCode saves the key in `~/.local/share/opencode/auth.json` (Windows: `%USERPROFILE%\.local\share\opencode\auth.json`), readable only by your user.

### A4. Choose a model and start working

- Type `/models` and pick a Blablador model (for example `alias-code`) or a de.NBI model.
- Press **Tab** to switch to the **Plan** agent, which plans without changing files. Switch back to build once you've read the plan.

To start OpenCode from VS Code, open the integrated terminal in your project folder and type `opencode`. With the extension you can also use:

| | Open OpenCode | New session |
|---|---|---|
| macOS | Cmd+Esc | Cmd+Shift+Esc |
| Linux | Ctrl+Esc | Ctrl+Shift+Esc |
| Windows | Click the OpenCode button | Click the OpenCode button |

On Windows these shortcuts don't reach VS Code: Ctrl+Esc opens the Start menu and Ctrl+Shift+Esc opens Task Manager.

### Why our laptop config asks before acting

By default, OpenCode lets the agent run shell commands, edit files and read or write **outside your project folder** without asking. Only reading `.env` files asks first. On your laptop that's too much, so our `opencode.json` and `opencode.no-plugin.json` contain:

```json
"permissions": [
  { "action": "shell", "resource": "*", "effect": "ask" },
  { "action": "edit", "resource": "*", "effect": "ask" },
  { "action": "external_directory", "resource": "*", "effect": "ask" }
]
```

See the [OpenCode permissions docs](https://opencode.ai/docs/permissions/).

> [!NOTE]
> OpenCode is made by a company that also sells paid model plans. You don't need them: Blablador and de.NBI are free for academics.

---

## Option B: VS Code's own chat with your key

VS Code's chat can use any OpenAI-compatible service with your own key (*bring your own key*, BYOK). You don't need a GitHub Copilot subscription for this.

### B1. Add Blablador

Follow the instructions in the [blablador-copilot-config repository](https://gitlab.jsc.fz-juelich.de/bischoff2/blablador-copilot-config). In short:

1. Open a **project folder** in VS Code first; the setup doesn't work without one.
2. Open the Command Palette (Cmd+Shift+P on macOS, Ctrl+Shift+P elsewhere) and run **Chat: Manage Language Models**.
3. Add a **Custom Endpoint** provider named `Blablador` with API type **Chat Completions**, and enter your Blablador key (the **legacy token** from Part 0) when asked.
4. VS Code opens `chatLanguageModels.json`. For the list of models, use **the `Blablador` block from our [`chatLanguageModels.example.json`](../configs/vscode/chatLanguageModels.example.json)**, not the one on the GitLab page: its model names are outdated and cause errors.

> [!IMPORTANT]
> **Don't edit the `"apiKey"` line yourself.** VS Code keeps your key in your system's secure storage and writes only a reference like `"${input:chat.lm.secret.…}"` into the file. Copy only the `"models"` list from our example. To change your key later: **Chat: Manage Language Models** → gear icon next to the provider → update the API key.

Where VS Code keeps `chatLanguageModels.json`, if you need to open it again:

- macOS: `~/Library/Application Support/Code/User/chatLanguageModels.json`
- Windows: `%APPDATA%\Code\User\chatLanguageModels.json`
- Linux: `~/.config/Code/User/chatLanguageModels.json`

Blablador's model names change from time to time. If a model stops working, check the current list in the Blablador docs.

### B2. Add de.NBI (optional)

Same steps, with a second Custom Endpoint provider named `de.NBI` and the `de.NBI` block from our example file. Create the key at <https://llm.bi.denbi.de/token-self-service/>.

> [!NOTE]
> In our tests de.NBI was not usable in VS Code: requests ran over the service's request budget because VS Code sends a lot of extra context. It works much better with OpenCode inside the VM.

### B3. Local or Copilot harness

At the bottom of the chat box you can choose how VS Code runs the agent:

- **Local** shows all your own models. It is **deprecated and will be removed in February 2027**.
- **Copilot** has more built-in features (good or bad, depending on your taste). To see your own models there, turn on the experimental setting `chat.agentHost.byokModels.enabled` (Settings → search for it).

If you have set things up in the Local harness before, migrate them in time:

- [Bring your own language model key](https://code.visualstudio.com/docs/agent-customization/language-models#_bring-your-own-language-model-key)
- [Move to the Copilot harness](https://code.visualstudio.com/docs/agents/run/move-to-copilot)
- [Migrate customizations](https://code.visualstudio.com/docs/agent-customization/migrate-customizations#_replace-chat-participants)

### B4. Inline code suggestions

Grey "ghost text" suggestions while you type come from GitHub Copilot itself, so they need you to be **signed in to GitHub**. Copilot is free for verified students and teachers ([GitHub Education](https://github.com/education/students)); others need a subscription.

---

## Another option: the Continued extension

The Blablador team recommends **[Continued](https://marketplace.visualstudio.com/items?itemName=AtaUlHaleem.continued)**, a VS Code extension developed at Forschungszentrum Jülich. (The original *continue.dev* extension is no longer open source.)

## Our verdict

- Blablador is much better documented and better supported than de.NBI. Both take some setting up, in similar ways.
- Between OpenCode and VS Code's own chat, we found OpenCode better.

---

[← 0. Sign up and install](0-sign-up-and-install.md) · Next: [2. Sandboxing with Multipass →](2-sandboxing-with-multipass.md)
