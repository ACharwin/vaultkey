# 🔐 VaultKey

A fully offline, open-source password manager built as a Progressive Web App (PWA). Runs entirely in your browser — no server, no cloud, no tracking.

**Live app → [acharwin.github.io/vaultkey](https://acharwin.github.io/vaultkey)**

---

## Features

- **100% Offline** — works with no internet after the first load
- **PIN Lock** — 6-digit master PIN with SHA-256 hashing
- **Biometric Unlock** — fingerprint / face unlock via WebAuthn
- **Full CRUD** — add, edit, delete accounts with name, username, password, URL, category, and notes
- **Password Generator** — with strength meter
- **Categories** — 6 built-in + unlimited custom categories with emoji
- **AES-256 Encrypted Backups** — backups are encrypted with your Master PIN before saving
- **Google Drive Backup & Restore** — save and restore encrypted `.vke` backups to your own Google Drive
- **Local Backup & Restore** — download/upload `.vke` encrypted backup files to your device
- **Persistent Storage** — uses IndexedDB with `navigator.storage.persist()` to prevent data eviction
- **Installable** — installable as a PWA on Android and desktop via Chrome

---

## Security

| Feature | Detail |
|---|---|
| PIN hashing | SHA-256 with salt |
| Backup encryption | AES-256-GCM |
| Key derivation | PBKDF2 — 100,000 iterations |
| Storage | IndexedDB — local device only |
| Data transmission | None — passwords never leave your device |
| Google Drive | Encrypted before upload — Google cannot read your data |

Your passwords are stored only on your device. Backups are encrypted with your Master PIN using AES-256-GCM before they are saved anywhere — locally or to Google Drive.

---

## Getting Started

### Use it instantly
Just open [acharwin.github.io/vaultkey](https://acharwin.github.io/vaultkey) in Chrome on Android or desktop.

### Install as an app (Android)
1. Open the URL in Chrome
2. Tap **⋮ menu → Add to Home screen**
3. The app will work fully offline from your home screen

---

## Backup & Restore

VaultKey supports two backup destinations:

### 📱 Local Backup
- Saves an encrypted `.vke` file to your device
- Restore by picking the file from your device

### ☁️ Google Drive Backup
- Signs into your Google account via OAuth
- Saves encrypted `.vke` file to `VaultKey/Backups/` in your own Drive
- Restore by signing in and selecting a backup from the list
- Google cannot read your data — it is encrypted before upload

> **Note:** All backups require your Master PIN to restore. If you forget your PIN, your backup cannot be decrypted.

---

## Backup File Format

Backups use the `.vke` (VaultKey Encrypted) format — a JSON file containing:

```json
{
  "vke": true,
  "version": 2,
  "iv": [...],
  "payload": [...]
}
```

The `payload` is AES-256-GCM encrypted. The `iv` is a random 12-byte initialization vector generated per backup.

Legacy `.vk` backups (unencrypted, version 1) are still supported for restore.

---

## Offline Support

VaultKey is a full PWA with a service worker that caches all app files on first load.

| Feature | Offline |
|---|---|
| View accounts | ✅ |
| Add / edit / delete | ✅ |
| Password generator | ✅ |
| Local backup & restore | ✅ |
| Google Drive backup | ❌ Needs internet |
| Google Drive restore | ❌ Needs internet |

---

## Tech Stack

- Vanilla HTML, CSS, JavaScript — zero dependencies, zero frameworks
- IndexedDB for persistent local storage
- Web Crypto API for AES-256-GCM encryption and PBKDF2 key derivation
- WebAuthn for biometric authentication
- Google Identity Services (GIS) for OAuth
- Google Drive API v3 for cloud backup
- Service Worker for offline PWA support
- Hosted on GitHub Pages

---

## Version History

| Version | Changes |
|---|---|
| v1.0 | Initial release — PIN lock, CRUD, categories, dashboard |
| v1.1 | Switched to IndexedDB + persistent storage |
| v1.2 | Fixed dashboard on first load, fixed form data leaking between records |
| v1.3 | Custom dialogs replacing all native alert/confirm/prompt |
| v1.4 | Reset vault 2-step confirmation, backup empty vault check |
| v1.5 | AES-256 encrypted backups, Google Drive backup & restore |
| v1.6 | PIN input masked in dialogs, reset vault fixed, syntax error fix |

---

## Privacy

- No analytics
- No tracking
- No ads
- No server
- No account required
- All data stays on your device

---

## License

MIT License — free to use, modify, and distribute.
