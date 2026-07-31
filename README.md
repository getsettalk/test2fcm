<div align="center">

<img src="./assets/images/logo.svg" width="88" alt="Test2FCM logo" />

# Test2FCM

### Firebase Cloud Messaging — Push Notification Testing Tool

Send **notification** and **data-only** push messages to one or many devices,
straight from your browser — now powered by the modern **FCM HTTP v1 API**.

`Firebase` &nbsp;·&nbsp; `FCM HTTP v1` &nbsp;·&nbsp; `Android` &nbsp;·&nbsp; `iOS` &nbsp;·&nbsp; `React-Native` &nbsp;·&nbsp; `Web Push` &nbsp;·&nbsp; `Vue.js` &nbsp;·&nbsp; `Open Source`

**🔗 Live tool → [getsettalk.github.io/test2fcm](https://getsettalk.github.io/test2fcm/)**

</div>

---

## 📸 Screenshots

<table>
  <tr>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/f11610ab-b0ef-4df7-930a-79cfb9daff1f" width="100%" alt="Light mode" /><br/>
      <sub><b>Light mode</b></sub>
    </td>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/9a98049f-3e4c-44ed-bb51-70318e58c295" width="100%" alt="Dark mode" /><br/>
      <sub><b>Dark mode (Firebase amber)</b></sub>
    </td>
  </tr>
</table>

---

## 🆕 What's new

Google **shut down the legacy FCM server-key API** (`fcm.googleapis.com/fcm/send`).
Test2FCM has been rebuilt on top of the **HTTP v1 API** and got a full redesign.

| Area              | Before (legacy)                  | Now (HTTP v1)                                                                |
| ----------------- | -------------------------------- | ---------------------------------------------------------------------------- |
| **Endpoint**      | `POST /fcm/send`                 | `POST /v1/projects/{projectId}/messages:send`                                |
| **Auth**          | Static **Server Key**            | **Project ID** + short-lived **OAuth 2.0 access token**                      |
| **Multi-device**  | `registration_ids` (multicast)   | One request **per token**, sent automatically in a loop                      |
| **Message types** | Notification only                | **Notification · Data-only · Both**                                          |
| **Saved data**    | Server key saved in localStorage | **Credentials** and **message templates** saved separately                   |
| **UX**            | Basic form                       | Responsive redesign, live JSON preview, per-device results, dark/light theme |

**Highlights**

- ✅ **HTTP v1 API** — future-proof, works directly from static hosting (GitHub Pages).
- ✅ **Data-only messages** — silent payloads your app handles in code.
- ✅ **Multi-device send** — paste many tokens (comma / space / new-line separated).
- ✅ **Built-in setup guide** — step-by-step Project ID + `gcloud` access-token help.
- ✅ **Live request preview** — see the exact JSON before you send it.
- ✅ **Per-device results** — clear delivered / failed status with error reasons.
- ✅ **Save profiles & templates** — reuse credentials and messages locally.
- ✅ **New look** — full-width navbar, Firebase-amber dark theme, fresh SVG logo/favicon.

---

## 🚀 Getting started

To send with the HTTP v1 API you need **two things**:

### 1. Project ID

1. Open the [Firebase Console](https://console.firebase.google.com/) → select your project.
2. Click the ⚙️ gear icon → **Project settings**.
3. Copy the value under **General → Project ID**.

### 2. Access Token (OAuth 2.0)

This is **not** your FCM device token. Generate a short-lived token with the [Google Cloud SDK](https://cloud.google.com/sdk/docs/install):

```bash
gcloud auth login
gcloud auth application-default login
gcloud auth print-access-token
```

Copy the printed token (it usually starts with `ya29…`) and paste it into the **Access Token** field.

> ⏱️ The access token expires in **~1 hour**. If sends start failing with `401 UNAUTHENTICATED`, just run `gcloud auth print-access-token` again and paste the new one.
>
> ⚠️ **Access Token ≠ Device Token.** The `APA91…` device token goes only in the **FCM Registration Token** field.

The in-app **Setup Guide** button walks you through all of this with copy-ready commands.

---

## 🧩 Message types

| Type             | What it sends                       | Use it for                               |
| ---------------- | ----------------------------------- | ---------------------------------------- |
| **Notification** | `notification` block (title + body) | A visible tray/banner notification       |
| **Data-only**    | `data` block only                   | Silent payloads handled in your app code |
| **Both**         | `notification` + `data`             | A visible notification plus custom data  |

Example request Test2FCM builds for you:

```json
{
  "message": {
    "token": "DEVICE_REGISTRATION_TOKEN",
    "notification": {
      "title": "Order shipped",
      "body": "Your package is on the way"
    },
    "data": { "orderId": "1234", "screen": "cart" },
    "android": { "priority": "high" },
    "webpush": { "fcm_options": { "link": "https://example.com/open" } }
  }
}
```

> ℹ️ In the `data` block, all values are automatically converted to **strings** (an FCM v1 requirement).

---

## 💾 Saved locally (in your browser)

Everything is stored in your own browser via `localStorage` — nothing is sent anywhere except Google's FCM endpoint:

- **Credentials** — save Project ID + access token as named profiles and load them in one click.
- **Message templates** — save a composed message (title, body, data, tokens, priority…) to reuse later.

---

## 🛠️ Tech stack

- **Vue 3** (via CDN — no build step)
- **vue-toast-notification** for toasts
- Plain, self-contained **HTML/CSS** (custom responsive design, light/dark theme)
- Hosted on **GitHub Pages**

The whole app is a single self-contained [`index.html`](./index.html) — clone and open it, or serve it with any static server.

```bash
# run locally
python3 -m http.server 4599
# then open http://localhost:4599
```

---

## 🤝 Contributing

This is an open-source project — contributions are welcome! Feel free to open an issue or a pull request to help make it better.

---

## 👤 Author

Built by **[Sujeet Kumar](https://github.com/getsettalk)**.

If this tool helped you, consider giving the repo a ⭐.
