# Config files

Ready-to-copy configuration files. **None of them contains an API key**, and none should: add your keys through each tool's key prompt, as the guides explain.

| File | For | Used in |
|---|---|---|
| [`opencode/opencode.json`](opencode/opencode.json) | OpenCode on your laptop: Blablador via plugin, de.NBI, asks before acting | [Part 1](../docs/1-ai-in-vscode.md#a2-add-the-configuration) |
| [`opencode/opencode.no-plugin.json`](opencode/opencode.no-plugin.json) | Same, with Blablador set up by hand instead of the community plugin | [Part 1](../docs/1-ai-in-vscode.md#a2-add-the-configuration) |
| [`opencode/opencode.vm.json`](opencode/opencode.vm.json) | OpenCode inside the VM: works without asking | [Part 2](../docs/2-sandboxing-with-multipass.md#option-a-opencode-recommended) |
| [`vscode/chatLanguageModels.example.json`](vscode/chatLanguageModels.example.json) | VS Code chat: the model lists for Blablador and de.NBI | [Part 1](../docs/1-ai-in-vscode.md#b1-add-blablador) |
| [`copilot-cli/providers.example.json`](copilot-cli/providers.example.json) | GitHub Copilot CLI with several models; you paste your keys in, inside the VM only | [Part 2](../docs/2-sandboxing-with-multipass.md#option-b-github-copilot-cli) |

Model names and limits change over time. If a model stops working, check the current list in the [Blablador docs](https://sdlaml.pages.jsc.fz-juelich.de/ai/guides/blablador_api_access/) or on <https://llm.bi.denbi.de/>.
