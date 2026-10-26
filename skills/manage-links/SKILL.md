---
name: manage-links
description: Find, change, archive or delete existing CodeQR short links and QR codes. Use when the person wants to see their links or QR codes, look one up, change where a printed QR code or a shared link leads, change a slug or an expiry date, archive one, or delete one.
---

# Manage links and QR codes

## Find

- `list_links` and `list_qrcodes` return the newest first, 20 per page unless `pageSize` asks for more (up to 100). Use `page` for the next page; when a reply says the page is full, there may be more. `list_links` also filters by `search`, `domain` and `tagId`.
- `get_link_info` looks up one link by `linkId`, by `externalId`, or by `domain` and `key` (for `codeqr.link/menu`: domain `codeqr.link`, key `menu`).

## Change where it leads

- Link: `update_link` with the `linkId` and the new `url`. Every copy already shared keeps working and now leads to the new address. Changing `key` rewrites the link itself and breaks every copy in circulation, so do it only when the person asks for that.
- Dynamic QR code: `update_qrcode` with the `qrcodeId` and the payload field of the type the code already has: `url` for a link code, `wifi` for a Wi-Fi code, and so on. A code cannot change type; check with `list_qrcodes` if unsure. Printed copies open the new content from then on.
- Static QR code: the content is in the printed pattern, so printed copies will never change. Say so before updating, and offer a new dynamic code instead.
- Other fields: on links, `expiresAt`, `comments`, `trackConversion`, the social preview (`proxy` with `title`, `description` and `image`) and `rules` (see the `smart-rules` skill); on QR codes, `fgColor`, `bgColor`, `title` and `walletPass`.

Before any change, tell the person what will change and where it shows, such as on printed material. The new destination must be a real address they gave.

## Archive or delete

- `archived: true` on either update tool hides the item from the default lists. It keeps working.
- `delete_link` and `delete_qrcode` cannot be undone: a deleted link stops resolving, and a printed QR code stops working for good. Before deleting, name what will stop working and wait for a clear yes.
