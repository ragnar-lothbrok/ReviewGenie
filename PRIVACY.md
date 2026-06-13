# ReviewGenie — Privacy Policy

**Effective date:** 2026-06-13
**Extension:** ReviewGenie – AI Doc Reviewer & Blueprint Engine
**Contact:** _Replace with your support email, e.g._ `raghunitb@gmail.com`

ReviewGenie is a "Bring Your Own Key" (BYOK) Chrome extension that helps you review Confluence pages with the AI provider **you** configure. We — the publisher of ReviewGenie — do **not** operate a backend, do **not** run analytics, and do **not** receive any of your data.

This policy explains exactly what data the extension touches, where it goes, and why each Chrome permission is requested.

---

## 1. Data we collect about you

**None.** ReviewGenie has no servers, no telemetry, no analytics SDKs, no advertising identifiers, no crash reporters, and no third-party trackers. The publisher cannot see your documents, your API key, your configuration, or your usage.

## 2. Data stored locally on your device

The following items are stored using Chrome's `chrome.storage.local` API and never leave your machine except as described in Section 3:

| Item | Purpose |
| --- | --- |
| AI provider selection (OpenAI / Anthropic / Azure / Custom) | Routes API calls correctly |
| API base URL, deployment name, API version, model name | Identifies the endpoint to call |
| **Your API key** | Authenticates calls to **your** AI provider |
| Last-analysis cache for the current page | Avoids re-sending the same page to your provider |

Uninstalling the extension removes all of the above. You can also clear it manually at any time via `chrome://extensions` → ReviewGenie → Details → "Extension options" or via Chrome's "Clear browsing data → Cookies and other site data".

## 3. Data sent to third parties

When **you** explicitly trigger an analysis (Analyze Page, Generate WBS, Security Scan, Test Plan, Optimize Doc, Architecture Review, Diagrams, Dependency Map, Requirements Breakdown, Alternatives, or Chat), the extension sends the following directly from your browser to the AI endpoint **you** configured:

- The text content of the active Confluence page (truncated to ~20,000 characters)
- Your prompt / chat message (if any)
- Your API key in the `Authorization` header

Recipients depend entirely on your settings:

- **OpenAI** → `https://api.openai.com/v1/...` (subject to [OpenAI's privacy policy](https://openai.com/policies/privacy-policy))
- **Anthropic** → `https://api.anthropic.com/...` (subject to [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy))
- **Azure OpenAI** → your tenant endpoint at `*.azure-api.net` / `*.openai.azure.com` (subject to your Microsoft agreement)
- **Custom Endpoint** → the URL you entered (subject to that operator's terms)

ReviewGenie does **not** proxy these requests. They are direct browser-to-provider HTTPS calls.

## 4. Confluence access

The content script runs only on URLs matching `https://*.atlassian.net/wiki/*`. It reads the rendered page (headings, prose, code blocks, embedded SQL, etc.) **only when you click an action** in the popup, side panel, or context menu. The extension does not exfiltrate Confluence content in the background, does not crawl other Confluence pages, and does not access Jira data.

## 5. Permissions justification

| Permission | Why it is needed |
| --- | --- |
| `activeTab` | Read the current Confluence page text when you click "Analyze". |
| `storage` | Persist your AI provider settings and API key locally. |
| `sidePanel` | Render analysis results in Chrome's native side panel. |
| `tabs` | Open the side panel and route messages to the correct tab. |
| `contextMenus` | Provide the right-click "Analyze with ReviewGenie" entry on Confluence pages. |
| `scripting` | Inject the content script that extracts the page text on demand. |
| `host_permissions` for `*.atlassian.net`, `*.atlassian.com` | Read Confluence page content (content script). |
| `host_permissions` for `*.openai.com`, `*.anthropic.com`, `*.azure-api.net`, `*.azure.com` | Make direct API calls to your selected provider. |
| `<all_urls>` | Allow the user-configured **Custom Endpoint** (self-hosted gateway, corporate proxy, etc.) to be any HTTPS URL. The extension only contacts the exact URL you save in Settings. |

## 6. What we do not do

- We do **not** sell, rent, or share any data.
- We do **not** use your documents or prompts to train any model.
- We do **not** include analytics, A/B testing, or fingerprinting libraries.
- We do **not** read browsing history or any non-Confluence tab.
- We do **not** auto-upload documents — every network call requires an explicit user action.

## 7. Security

- Your API key is stored in `chrome.storage.local`, isolated to the extension's origin.
- All outbound calls use HTTPS.
- No remote code is loaded; the extension ships with all scripts bundled.

## 8. Children's privacy

ReviewGenie is a developer productivity tool not directed to children under 13 and does not knowingly collect data from them.

## 9. Changes to this policy

Material changes will be reflected by updating the "Effective date" at the top and noted in the extension's release notes on the Chrome Web Store listing.

## 10. Contact

For questions or data requests: _Replace with your support email_ — `support@yourdomain.com`

---

> **Publisher checklist before submission**
> 1. Replace the contact email above with a real, monitored address.
> 2. Host this file at a public HTTPS URL (e.g., GitHub Pages, your domain) and paste that URL into the **Privacy policy URL** field of the Chrome Web Store Developer Dashboard.
> 3. In the Dashboard's **Privacy practices** tab, declare a "Single purpose": _Review and improve technical documents on Confluence using a user-configured AI provider._
> 4. Declare data usage as: **Website content** (used for the single purpose, not sold, not used for credit/advertising, not used for unrelated purposes).
