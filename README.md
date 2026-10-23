# hava-feed

Static, **signed** news & update feed for **Hava / هوا** — a native Android weather app (Persian + English, Jalali calendar, many weather sources).

این مخزن فقط فایل‌های ایستای «هوا آنلاین» را نگه می‌دارد: یک `feed.json` امضاشده (Ed25519) و یک صفحهٔ معرفی ساده.

## What is here

| File | Purpose |
|---|---|
| `feed.json` | Signed feed (news, update info, mirror list). The app verifies the signature on-device with public keys baked into the APK; a file that was edited by hand, or served by anyone else, is rejected. |
| `index.html` | Small public page (no scripts, no trackers, no external requests). |
| `robots.txt` | Allow all. |

## Notes

- The app downloads nothing else from here and sends **no** personal data: a plain `GET feed.json`, no cookies, no identifiers.
- Updates are only installed after the user taps *Install* and Android shows its own confirmation; the APK is checked against the SHA-256 and the signing certificate pinned in the signed feed.
- Please do not edit `feed.json` by hand — it will simply fail verification.

Made by **Parsa** — Telegram: [@Im_Troller](https://t.me/Im_Troller). All rights reserved © 2026 Parsa.
