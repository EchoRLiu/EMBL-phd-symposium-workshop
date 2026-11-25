# 0. Sign up and install

[← Back to overview](../README.md) · Next: [1. AI in VS Code →](1-ai-in-vscode.md)

- [Blablador: account and API key](#blablador-recommended)
- [de.NBI: account and API key (optional)](#denbi-optional)
- [VS Code](#vs-code)
- [Git](#git)
- [GitHub account](#github-account)
- [Multipass](#multipass)

---

## Blablador (recommended)

Blablador is the LLM service of Helmholtz AI. It is free for academics and offers both a chat website and an API.

### Create an account

1. Go to <https://helmholtz-blablador.fz-juelich.de/login>.
2. Click **Login**.
3. Under *Login using external account*, click **Helmholtz ID**.
4. **Recommended:** search for your institution in the search bar. If you find it, log in with your institute account. You then only need to accept a few terms and can use Blablador right away.
5. If your institution isn't listed, search instead for:
   - **ORCID** (recommended), or
   - **GitHub**, or
   - **Google**

   and log in with those credentials. You may need to accept some terms.

   > ⚠️ **Gmail doesn't work.** Blablador blocks accounts registered with a Gmail address, including a GitHub account that uses one.
   > The GitHub and Google options can also be buggy: even after a successful confirmation, you may be sent back to this step again and again. If that happens, use ORCID.
6. The first time, you see a *First time login* window saying *"Your authentication with remote service was successful; however, your account is not known here"*. Click **Register** and complete the check that you're not a bot.
   If you registered before, you are logged in directly.
7. You'll receive an email within a few minutes. Click the link in it to confirm your registration.
8. You can now log in.

### Create your API key

Blablador uses a token from the Helmholtz GitLab ([Helmholtz Codebase](https://codebase.helmholtz.cloud)) as its API key.

1. Open <https://codebase.helmholtz.cloud/-/user_settings/personal_access_tokens> (or: your profile picture, top right → **Preferences** → **Access** → **Personal access tokens**).
2. Click **Add new token** and choose a **legacy token**.
3. Give it a name, for example `Blablador API key`.
4. Set an **expiration date**. Tokens last at most one year; a few months is enough for the workshop.
5. Select **only** the **`read_user`** scope.
6. Create the token and **copy it straight into your password manager**. GitLab shows it only once.

> [!CAUTION]
> This token belongs to your Helmholtz GitLab account. Give it **only** the `read_user` scope. A token with `api` or `write_*` scopes would let anyone who has it, including an AI agent, change your GitLab projects.

The API address is `https://api.blablador.fz-juelich.de/v1`.

<details>
<summary>Rate limits (useful to know for coding agents)</summary>

Coding agents send many requests. Blablador limits requests per minute for each model name:

| Model name | Requests per minute |
|---|---|
| `alias-fast` | 60 |
| `alias-code`, `alias-large` | 40 |
| `alias-huge` | 30 |
| Any other model name | 20 |

The `alias-…` names therefore give you more room. If you go over the limit you get a `429` error and have to wait. Repeated violations lead to longer waits. See the [Blablador API documentation](https://sdlaml.pages.jsc.fz-juelich.de/ai/guides/blablador_api_access/).
</details>

---

## de.NBI (optional)

The de.NBI Cloud Bielefeld LLM API is **API-only**: there is no chat website.

> [!IMPORTANT]
> You need a **Life Science Login linked to a German research institution**; your email domain counts. Access is managed through de.NBI projects with a responsible principal investigator. If you can't get access, use Blablador.

### Create an account

1. Go to <https://llm.bi.denbi.de/>.
2. Click **Single Sign-On**.
3. Click **LS Login**.
4. **Recommended:** search for your institution and log in with your institute account.
   Other options are **GitHub**, **ORCID** and **Google**. Sign-in with these can be buggy, so you may have to try a few times.
5. The first time, you're asked to **Proceed to register for an account**:
   1. Fill out the application form and submit it. A confirmation email arrives within a few minutes.
      **Don't close the tab** where you submitted the form: after you click the link in the confirmation email, the *Life Science Login Activation* page updates in that tab.
   2. On the *Life Science Login Activation* page, select **Approved** and submit to activate the account.
   3. Wait for an email titled **"Access granted: llm.bi.denbi.de"**. This can take about 20 minutes. (When signing up with ORCID, this email never arrived in our test.)
   4. Log in again with the same method and accept the remaining terms. If a page says approval is still needed, refresh it.
6. Create your API token at <https://llm.bi.denbi.de/token-self-service/> and store it in your password manager.

The API address is `https://llm.bi.denbi.de/v1`.

### Blablador or de.NBI?

- Blablador is much smoother to sign up for, better documented and better supported by the tools below.
- Blablador also has a chat website; de.NBI is API-only.
- Both are zero-retention services. Still, don't send personal, patient or unpublished confidential data to any hosted model.

---

## VS Code

- Download: <https://code.visualstudio.com/download>
- Helpful extension: **Git Graph**, to see your commits and branches.

## Git

You should always track your code with Git: it's your undo button when an agent changes things.

- Download for macOS, Windows or Linux: <https://git-scm.com/downloads>

> [!TIP]
> **Windows only:** the code you edit on Windows will also be used inside a Linux VM. To avoid line-ending problems, run this once after installing Git, before you clone anything:
>
> ```powershell
> git config --global core.autocrlf input
> ```
>
> Without it, shell scripts can fail inside the VM with errors like `$'\r': command not found`.

## GitHub account

- Sign up at <https://github.com/>.
- Students and teachers can get GitHub Copilot for free through [GitHub Education](https://github.com/education/students).
- You need a GitHub sign-in only for Copilot's **inline code suggestions** in VS Code. Chat with your own Blablador or de.NBI key works without it.

## Multipass

Multipass creates Ubuntu virtual machines with one command. You need **version 1.17.2 or newer**.

| Your laptop | How to install |
|---|---|
| macOS | Installer from <https://canonical.com/multipass> (or the zipped installer from [GitHub releases](https://github.com/canonical/multipass/releases)) |
| Windows | Installer from <https://canonical.com/multipass> (or the zipped installer from [GitHub releases](https://github.com/canonical/multipass/releases)) |
| Ubuntu | `sudo snap install multipass` |
| Other Linux | First [install snapd](https://snapcraft.io/docs/tutorials/install-the-daemon/), then `sudo snap install multipass` |

Check the version:

```bash
multipass version
```

<details>
<summary><b>Windows requirements</b></summary>

- Windows 10 or 11, version 1809 or newer. Home, Pro and Enterprise all work: since Multipass 1.17 the default Windows driver (HCS) no longer needs Hyper-V or Windows Pro.
- The Windows feature **Virtual Machine Platform** must be turned on: search the Start menu for *Turn Windows features on or off*, tick **Virtual Machine Platform**, and restart.
- Virtualisation must be enabled in your computer's BIOS/UEFI (usually it is).
- Older Multipass installs that used Hyper-V or VirtualBox: see [Migrate from Hyper-V to the HCS driver](https://canonical.com/multipass/docs/stable/how-to-guides/customise-multipass/migrate-from-hyperv-to-hcs-on-windows/).
</details>

> [!TIP]
> The first VM you launch downloads an Ubuntu image, which takes a while. Do it once before the workshop:
> `multipass launch --name warmup`, then `multipass delete --purge warmup`.

---

[← Back to overview](../README.md) · Next: [1. AI in VS Code →](1-ai-in-vscode.md)
