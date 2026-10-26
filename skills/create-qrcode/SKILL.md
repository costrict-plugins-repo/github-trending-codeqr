---
name: create-qrcode
description: Create a QR code with CodeQR. Use when the person wants a QR code for a website, menu, flyer, poster or packaging, a Wi-Fi network, a contact card (vCard), a WhatsApp chat, an email, an SMS, a phone number, plain text or a crypto payment request, or a code they can still change after printing.
---

# Create a QR code

Use the CodeQR connector's `create_qrcode` tool. Set `type`, then fill the payload field with the same name:

| `type` | Payload | Watch out for |
|---|---|---|
| `url` (default) | `url` | The real destination. Ask if it is missing; never use a placeholder such as example.com |
| `wifi` | `wifi.ssid`, `wifi.password`, `wifi.encryption` | `encryption` is `WPA`, `WPA2`, `WEP`, or `nopass` for an open network |
| `vcard` | `vcard.name`, `surname`, `phone`, `email`, `website`, `address`, `city`, `state`, `zipcode`, `country` | City, state, zipcode and country are only encoded when `address` is given too |
| `whatsapp` | `whatsapp.number`, `whatsapp.message` | Number in E.164 without `+` or separators, such as `5511999999999` |
| `email` | `email.email`, `subject`, `body`, `cc`, `cco` | BCC goes in `cco`, not `bcc` |
| `sms` | `sms.tel`, `sms.subject` | `subject` holds the message text |
| `phone` | `phone` | Include the country code |
| `text` | `text` | |
| `crypto` | `crypto.cryptocurrency`, `crypto.address`, `amount`, `message` | The wallet goes in `address` |

## Dynamic or static

A code is dynamic unless the person asks otherwise: it encodes a CodeQR short link, so what it opens can be changed later with `update_qrcode` without reprinting, and every scan is counted.

Only when the person asks for a static code, and only for `wifi`, `vcard` or `text`, set `static: true`. The content is then encoded in the pattern itself: it can never be changed once printed, and its scans are not counted. Say this before creating it. A static Wi-Fi code needs `encryption`, and `password` unless the network is open.

## Appearance

All optional: `fgColor` and `bgColor` as hex, `size` in pixels, error correction `level` (`L`, `M`, `Q` or `H`), `title`, and `domain` and `key` for the short link underneath. `walletPass` puts the person's own name, logo and barcode text on the Google or Apple Wallet pass saved from the code, on plans that include custom wallet branding.

## Reply

Give the QR code's ID, what it opens and, for a dynamic code, the short link it encodes. When the connector shows a card for the code, keep the text to what the card does not say.
