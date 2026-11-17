# Allowlist the ChatGPT cloud browser

A Codex skill for website operators who want Dots and ChatGPT Work to reach their site when a CDN or firewall challenges verified cloud browser traffic. It covers Cloudflare, Akamai, HUMAN, Vercel and providers that verify Web Bot Auth signatures directly. The provider steps follow [OpenAI’s cloud browser allowlisting guide](https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting).

## Install in Codex

Ask Codex to install the skill from this repository.

```text
Use $skill-installer to install the skill at https://github.com/jameszsun/allowlist-chatgpt-cloud-browser/tree/main/allowlist-chatgpt-cloud-browser
```

To install it manually, extract the [skill ZIP](https://github.com/jameszsun/allowlist-chatgpt-cloud-browser/raw/refs/heads/main/allowlist-chatgpt-cloud-browser.zip) into `~/.agents/skills/`. To share it within a project, extract the ZIP into the project’s `.agents/skills/` directory. [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills)

## Use it

```text
Use $allowlist-chatgpt-cloud-browser to walk me through allowing Dots and ChatGPT Work to access example.com. We use Cloudflare.
```

If browser use is disabled, Codex asks which provider handles bot blocking and gives that provider’s instructions directly in chat. If you already named the provider, it goes straight to the steps.

## Verify access

Test Dots and ChatGPT Work separately. If your site has a sign-in flow, ask each product to try it with an authorized account. Enter credentials or complete MFA in the site’s own sign-in flow. A visible account menu can confirm authenticated access. If the session was already signed in, record that detail. If sign-in stops, record the step it reached.

For a site with no sign-in path, ask each product to open the same public URL and report a recognizable heading. The [skill instructions](allowlist-chatgpt-cloud-browser/SKILL.md) include the test prompt and guidance for tracking down a block.
