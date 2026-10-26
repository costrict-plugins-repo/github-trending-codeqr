---
name: organize-workspace
description: Check which CodeQR workspace and plan the connection uses, see the workspace's custom domains, and list or create tags. Use when the person asks which workspace or plan they are on, which domains they can use for links, or wants to organize links with tags.
---

# Workspace, domains and tags

- `get_workspace` returns the name, slug and plan of the workspace this connection is authorized for. Call it before creating many items, or before using a feature the plan may not include.
- `list_domains` lists the workspace's custom domains. Shared short domains are not listed, and leaving `domain` out when creating a link or QR code uses the workspace's default. Adding or verifying a domain needs DNS records and is done in the CodeQR dashboard, not through the connector.
- `list_tags` and `create_tag` manage tags. A tag's color is one of `red`, `yellow`, `green`, `blue`, `purple`, `pink` or `brown`. Pass tag IDs as `tagIds` to `create_link`, and filter `list_links` by `tagId`.
- The connection reaches one workspace, picked when the person signed in to CodeQR. To work in another one, they reconnect CodeQR from the app's connector settings and pick it.
