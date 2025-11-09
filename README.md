# EasyFlag — Amazon Internal Helper

Ultra-clean userscript to streamline Content Symphony QA and SIM ticket creation.

---

## 🚀 Overview

**EasyFlag** is a Tampermonkey userscript that improves two workflows:

1. **Retail Homepage Overlay** — Adds small clickable flag buttons on Amazon homepages (FR, DE, UK, etc.) that link directly to each creative in **Content Symphony**.
2. **Content Symphony Widget** — Displays a floating widget inside CS to auto-generate **SIM tickets** using AI (Claude 3 Haiku via AWS Bedrock).

Both features aim to make QA and flagging issues drastically faster and standardized.

---

## 🧩 Features

* 🏷️ **Auto Flag Overlay** on retail sites for one-click CS access.
* 🧠 **AI Ticket Generation**: Paste an issue → get a ready-to-send SIM ticket draft.
* 🔐 **Bedrock Integration**: Works with short-term API keys.
* 🌍 **Locale Support**: FR, UK, DE, ES, IT, SE, PL, TR, NL, BE.
* 🪶 **Owner/Team Auto-detection** inside CS.
* ⚙️ **Prefilled SIM Redirect** with title, description, and marketplace field.
* 💾 **Key Persistence** via Tampermonkey storage.
* 🎛️ **Visibility Toggle (Alt+L)** on homepages.

---

## 🏗️ Installation

1. Install **[Tampermonkey](https://www.tampermonkey.net/)** on your browser.
2. Create a new userscript → paste the code from this repo.
3. Save and enable it.
4. Visit any Amazon retail homepage or Content Symphony placement page to verify.

---

## 🧠 How It Works

### Retail Homepage Overlay

* Runs on all major Amazon TLDs.
* Detects creative placement IDs from DOM attributes (`pf_rd_p`, `data-csa-c-content-id`).
* Builds direct CS creative URLs:
  `https://console.harmony.a2z.com/content-symphony/EU/placements/<PID>/redirectToCreative`
* Injects a flag icon over each creative.
* Floating toggle (bottom-right) and **Alt+L** shortcut control visibility.

### Content Symphony Widget

* Appears automatically on CS creative pages.
* Collects: **Issue**, **Bedrock Key**, and **Locale**.
* Detects **Owner** and **Business Group** using XPath.
* Builds an LLM prompt → calls Bedrock Runtime (Claude 3 Haiku) → displays formatted SIM ticket.
* “Go SIM” copies the text and opens a prefilled **SIM issue** page.

---

## 🧪 Testing

1. Open an Amazon homepage → flags appear.
2. Click a flag → redirects to CS creative.
3. Open a CS placement → EasyFlag widget appears.
4. Paste Bedrock API key, write an issue, pick locale, click **Generate**.
5. AI produces a formatted SIM ticket.
6. Click **Go SIM** → prefilled issue opens.

---

## ⚙️ Configuration

| Variable            | Description                              |
| ------------------- | ---------------------------------------- |
| `REGION`            | Hardcoded Bedrock region (`us-east-1`)   |
| `MODEL_ID`          | `anthropic.claude-3-haiku-20240307-v1:0` |
| `CS_REGION`         | Hardcoded to `EU` for now                |
| `SIM_FOLDER`        | `e3306293-dbb4-498d-9ea5-63d093bb5477`   |
| `LOCAL_STORAGE_KEY` | `ftc_links_visible`                      |
| `GM Keys`           | `sim3_api_key`, `sim3_locale`            |

---

## 🪲 Common Issues

* **Flags not visible:** Ensure page matches `@match` and has creative containers (`.gw-col`, `.celwidget`).
* **Owner not detected:** XPath outdated → update in script.
* **Bedrock call fails:** Invalid/expired API key or region mismatch.
* **SIM redirect wrong:** Verify query params in `SIM_URL` builder.

---

## 🔒 Security Notes

* Bedrock API key stored locally only via Tampermonkey storage.
* No data sent to third parties.
* External icons are CDN-hosted — replace with internal assets if required.

---

## 🧰 Developer Notes

* Uses Mustache.js for templating prompts.
* MutationObserver + debounce for DOM injection.
* WeakSet prevents duplicate link injection.
* 60s timeout for Bedrock requests.

---

## 🧭 Future Improvements

* Dynamic CS region detection (EU/NA/APAC).
* Optional non-persistent API key mode.
* LLM fallback model selector.
* Inline validation before SIM redirect.
* Internal hosting for assets.

---

## 🧑‍💻 Author & Ownership

**Built by:** FR I&I Team — @dutrey
**Current Version:** 2.0
**Model:** Claude 3 Haiku (Bedrock)

---

## 📄 License

Internal Amazon project — do not distribute outside internal network.
