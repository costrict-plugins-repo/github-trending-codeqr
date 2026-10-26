# CodeQR - Link and QR Analytics

Create dynamic QR codes and branded short links from a conversation with Claude, change where they lead after they are printed or shared, and read their scan and click analytics.

The plugin connects Claude to [CodeQR](https://codeqr.io)'s hosted MCP server and adds skills that tell Claude how to use it well: which fields each kind of QR code needs, when a code should be static, how smart rules and A/B splits are written, and what an update or a delete does to codes already in circulation.

## What you can ask for

- "Make a QR code for our menu at https://… that I can change later without reprinting."
- "Create a Wi-Fi QR code for the shop: network Shop-Guest, password …, WPA2."
- "Shorten https://… as go.mybrand.com/spring with a custom social preview."
- "Send iPhone visitors of this link to the App Store and Android visitors to Google Play."
- "Split traffic on this link 50/50 between these two landing pages, then tell me which one wins."
- "How many times were my QR codes scanned in the last 30 days, and from which cities?"
- "Change the QR code on our flyers so it opens the new booking page."

## Skills

| Skill | What it covers |
|---|---|
| `create-link` | Short links with a custom slug or domain, tags, expiry, password, social preview and conversion tracking |
| `create-qrcode` | QR codes for URLs, Wi-Fi, contact cards, WhatsApp, email, SMS, phone numbers, text and crypto payment requests; dynamic or static |
| `smart-rules` | Routing by device, country, city, region, continent, language, referrer or UTM, A/B splits, results per variant, ending a test |
| `analytics` | Scans, clicks, leads and sales over time and by country, city, device, browser, operating system, referrer and top performers |
| `manage-links` | Finding, changing, archiving and deleting links and QR codes |
| `organize-workspace` | The connected workspace and plan, custom domains and tags |

In Claude Code and Cowork, `/codeqr:codeqr <request>` routes a request to the right skill.

## Connect your CodeQR account

The plugin uses CodeQR's MCP server at `https://mcp.codeqr.io/mcp`, the same server as the CodeQR connector in the Claude directory. There is no API key to create or paste. The first time Claude uses a CodeQR tool, you sign in to CodeQR in your browser, choose the workspace Claude may use, and approve. In claude.ai and Cowork, connect it from the plugin's **Connectors** tab; in Claude Code, run `/mcp` to start the sign-in.

You need a CodeQR account; the free plan works. Smart rules, conversion tracking, long analytics windows and custom wallet pass branding depend on your plan, and Claude tells you when a request goes beyond it.

To revoke access, remove the integration under **Settings → Integrations** in the CodeQR dashboard. Connecting CodeQR to another app replaces the earlier authorization, so reconnect here if you use several.

## Data

- When Claude calls a CodeQR tool, the arguments it chose go to `mcp.codeqr.io`, which calls the CodeQR API (`api.codeqr.io`) with your workspace's OAuth token. These are what the code or link is made of: destination URLs, QR code content such as Wi-Fi credentials or contact details, link settings, tag names and analytics filters.
- CodeQR stores the links, QR codes and tags you create in your workspace, and records each scan and click (time, country, city, device, browser, referrer) for your analytics.
- The MCP server keeps operational logs of which tool ran, whether it succeeded and how long it took. It does not log argument values.
- The plugin itself is Markdown and JSON. It runs no code on your machine and stores nothing locally.

Privacy policy: [codeqr.io/en/privacy](https://codeqr.io/en/privacy). Terms: [codeqr.io/en/terms](https://codeqr.io/en/terms).

## Documentation and support

- MCP server and tool reference: [docs.codeqr.io/mcp/introduction](https://docs.codeqr.io/mcp/introduction)
- Help center: [codeqr.io/en/help](https://codeqr.io/en/help)
- Support: contact@codeqr.io

## Develop

```bash
claude plugin validate ./codeqr-plugin
claude --plugin-dir ./codeqr-plugin
```

## License

MIT. See [LICENSE](LICENSE).
