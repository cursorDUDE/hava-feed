# hava-feed — static files for the Hava weather app

This repository holds the public, **static** files that the Android app **Hava · هوا** reads. There is no server program, no database and no account behind it.

| path | what it is |
|---|---|
| `feed.json` | the signed news / "new version" file the app polls (an envelope: `kid`, base64 `payload`, ECDSA `sig`) |
| `apk/Hava-<version>.apk` | the official release APKs referenced by the signed feed |
| `index.html` | a small public page that shows `feed.json` (a courtesy — it does **not** verify the signature) |
| `.well-known/security.txt` | how to report a vulnerability |

## Nothing here is trusted by the app

Everything the app accepts from this repository is checked **inside the app** with keys compiled into the APK:

* `feed.json` is signed with **ECDSA P-256 / SHA-256** (domain-separated: `"hava-feed-v1\n" + payload`) by the publisher key `k2`, or by the offline root key `r2` in emergencies. A wrong, old or tampered file is ignored.
* An update is installed only if the downloaded file matches the **size and SHA-256 written in the signed feed**, has the package name `app.hava`, a higher version code, and is signed by **the same certificate as the installed app** — and Android's installer still asks the user.
* If this repository or its CDNs were taken over, the worst case is that updates stop arriving.

Official signing certificate (SHA-256) of every Hava release:
`2a:24:2b:ca:87:79:2d:48:cc:eb:1a:d0:0f:50:30:1d:17:e1:aa:16:f9:a5:d4:11:f3:5b:61:5f:d3:62:c6:50`
Check a downloaded file with `sha256sum Hava-*.apk` (compare with `latest.sha256` shown on the page) and `apksigner verify --print-certs Hava-*.apk`.

## Addresses

* GitHub Pages: `https://cursordude.github.io/hava-feed/feed.json`
* jsDelivr (CDN, caches `@main` up to 12 h): `https://cdn.jsdelivr.net/gh/cursorDUDE/hava-feed@main/feed.json`
* raw: `https://raw.githubusercontent.com/cursorDUDE/hava-feed/main/feed.json`

## Credit and contact

Hava is designed and built by **Parsa** — Telegram [@Im_Troller](https://t.me/Im_Troller). All rights reserved © 2026 Parsa.
Security reports: message me on Telegram privately (see `.well-known/security.txt`).

---

**فارسی:** این مخزن فقط فایل‌های ایستای برنامهٔ هوا را نگه می‌دارد (خبر و اعلام نسخهٔ جدید با امضای دیجیتال). برنامه چیزی را از اینجا بدون بررسی امضا نمی‌پذیرد؛ اگر این مخزن هم هک شود، بدترین حالت این است که به‌روزرسانی‌ها نرسند. اثر انگشت گواهی رسمی بالا را با `apksigner verify --print-certs` مقایسه کنید.
