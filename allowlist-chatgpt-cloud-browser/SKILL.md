---
name: allowlist-chatgpt-cloud-browser
description: Help website operators allow verified Dots and ChatGPT Work cloud browser visits through their CDN or firewall. Use for site allowlisting, Web Bot Auth setup, or troubleshooting a blocked cloud browser visit.
---

# Allow Dots and ChatGPT Work to visit a website

## Start the walkthrough

When browser use is disabled or unavailable, switch straight to instructions in chat. If the operator has not named their bot-blocking provider, offer the walkthrough and ask which provider they use.

> I can walk you through the settings here. Which provider handles bot blocking for your site (Cloudflare, Akamai, HUMAN, Vercel, or another provider)?

If they are unsure, suggest checking which dashboard logged the challenge or asking whoever manages the site’s firewall. Hosting and bot protection can come from different providers. Once the provider is known, give its steps below directly. If it was named in the request, start with those steps immediately.

When browsing is available and permitted, check the [current OpenAI Help Center guide](https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting) for the latest settings. The [OpenAI developer guide](https://developers.openai.com/commerce/agent-access) also covers these providers. If the guides are unreachable, use the steps below.

## Find the applicable setting

Give the operator the path for the service enforcing the policy. These settings were checked on November 16, 2026.

- **Cloudflare.** Select the site’s zone. In **Security → Settings**, filter for **Bot traffic** and open **AI Crawler and Agent access policies**. Find **dots, OpenAI** in **Personal Agents**, choose **Allow (do not block)**, then save. If the site uses WAF custom rules for exceptions, open **Security → WAF**, create a rule where **Bot Detection ID** equals **129220581** (listed as **ChatGPT Operator**), and scope the allow or skip action to the blocking control. Save and deploy.
- **Akamai.** In the site’s **Security Configuration**, open **Shared Resources → Custom Bot Categories**. Create and save a category, then add **ChatGPT Agent** with type **Verified Bots**. Open the active security policy and, under **Bot & Agent Control → Custom Bots**, set that category to **Allow**.
- **HUMAN.** In Sightline or BD, open **Policies → Traffic Policy Settings → Known Bots & Crawlers**. Find **ChatGPT Agent**, turn its rule **ON** and choose **Allow**. For AgenticTrust, open **Policies → AI Agents Permissions** in Sightline, select **ChatGPT Agent**, and grant the permissions the operator wants.
- **Vercel.** Vercel automatically verifies the agent. If Vercel handles bot protection, run the access test below. If a visit is blocked, check the matching firewall event for a custom rule or an upstream provider.
- **Other CDNs or firewalls.** For a provider without built-in Web Bot Auth support, have the edge verifier match the `Signature-Agent` value to `"https://chatgpt.com"`, including the quotes. Retrieve the matching key from [OpenAI’s public key directory](https://chatgpt.com/.well-known/http-message-signatures-directory) and validate `Signature` and `Signature-Input` per [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421.html). Grant the exception only after verification succeeds. All other requests follow the site’s usual policy.

For a walkthrough, give the steps for that site and link the guide. For a requested configuration change, use the site’s existing dashboard or infrastructure-as-code workflow, apply only the authorized change, and identify whether it is proposed or deployed. Keep other bot rules and application access controls in force. If the requested browsers already pass the applicable access test below, report that result.

## Verify access in Dots and ChatGPT Work

Test each requested product in its own cloud browser. Use the site's known sign-in URL or follow its normal account or SSO link. If the entry point is unclear, check the site's navigation or ask the operator where users sign in. Use a public-page visit as the test only when the operator or site confirms there is no sign-in path.

When browser use is disabled, give the operator this prompt for each product and leave the test pending. Fill in the site or sign-in URL when known.

> Use your cloud browser to go to [site or sign-in URL] and try to sign in with my authorized account. Hand control to me in the sign-in flow if I need to enter credentials or complete MFA. Tell me whether you reached the signed-in area or where you stopped. If the site has no sign-in path, visit [public page on the same site] and report its main heading.

Confirm successful sign-in with a non-sensitive indicator such as an account menu or a sign-out control. If the session was already signed in, report that authenticated access was verified through the existing session. If the product cannot sign in, credentials or MFA are pending, or the site challenges the attempt, report the furthest step reached and leave sign-in unverified. Keep credentials and one-time codes in the site's sign-in flow.

Report the outcome for Dots and ChatGPT Work separately. For a site with no sign-in path, record the public URL and a recognizable heading. For a suspected bot block, match the time and hostname of the failed step to the edge event. Check the rule, the verified agent match and whether proxies preserved `Signature`, `Signature-Input` and `Signature-Agent`. Retry the same failed step after correcting the identified cause.
