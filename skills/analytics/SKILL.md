---
name: analytics
description: Read CodeQR scan and click analytics. Use when the person asks how many times a QR code was scanned or a link was clicked, where the traffic came from (country, city, device, browser, operating system, referrer), how it changed over time, which links or QR codes perform best, or how many leads and sales a link produced.
---

# Analytics

Use the CodeQR connector's `get_analytics` tool. `event` and `groupBy` are required.

## Event

- `scans` for QR codes, `clicks` for short links.
- `leads` and `sales` for links with conversion tracking on. The connector reads these counts but cannot record a lead or a sale; the person's own site or backend sends those to CodeQR.
- `composite` for clicks, leads and sales together.

## Scope

- One QR code: `qrcodeId`, from `list_qrcodes`.
- One link: `linkId`, from `list_links`, or `domain` and `key` for a short link the person pastes. For `codeqr.link/menu`, the domain is `codeqr.link` and the key is `menu`.
- Neither: the whole workspace.

## Grouping

`count` for a total, `timeseries` for a trend, `countries`, `cities`, `devices`, `browsers`, `os` and `referers` for where the traffic came from, and `top_links`, `top_qrcodes` and `top_urls` for what performed best.

## Period

`interval` is `1h`, `24h` (the default), `7d`, `30d`, `90d`, `ytd`, `1y` or `all`. Long windows are not available on every workspace and come back as an error instead of data. When that happens, ask again with a shorter interval and say which period the answer covers.

## Reply

Answer the question that was asked, with the number and the period it covers. For a breakdown, give the top few rows. Do not paste raw JSON. When the connector shows an analytics card, keep the text short.
