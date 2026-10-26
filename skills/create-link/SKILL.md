---
name: create-link
description: Create a CodeQR short link. Use when the person wants to shorten a URL, make a branded or trackable link, set a custom slug, domain, expiry date or password, give a link its own social preview, or turn on conversion tracking for a link.
---

# Create a short link

Use the CodeQR connector's `create_link` tool.

1. Get the real destination. If the person has not given the address the link should open, ask for it. Never invent one or use a placeholder such as example.com: CodeQR refuses those and nothing is created.
2. Fill in only what the person asked for:
   - `key`: a custom slug, such as `spring-menu`. Left out, CodeQR generates one.
   - `domain`: one of the workspace's custom domains. Call `list_domains` when they name a domain or ask which ones they have. Left out, the workspace's default short domain is used.
   - `tagIds`: IDs from `list_tags`. If the tag does not exist yet, create it with `create_tag` first.
   - `expiresAt` (ISO 8601), `password`, `comments` (internal notes) and `externalId` (their own reference for the link).
   - Social preview: `proxy: true` together with `title`, `description` and `image` in the same call. `proxy` on its own renders an empty preview card.
   - `trackConversion: true` when they want leads and sales attributed to the link. It appends a `cq_id` parameter to the destination, and it is only available on plans with conversion tracking: on other plans the whole call is refused.
   - `rules`, to send visitors to different pages by device, country or language, or to split traffic for an A/B test: follow the `smart-rules` skill.
3. Reply with the short link, where it leads and its ID. Mention that the destination can be changed later and the link keeps working. Do not paste the full API response.

## When the call is refused

- A limit of the workspace comes back as a sentence with a details link. Relay it plainly and offer the version of the request that fits, such as the same link without `trackConversion` or `rules`.
- A placeholder refusal means you still need the real address from the person.
