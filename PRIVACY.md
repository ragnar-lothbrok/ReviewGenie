<!-- https://github.com/ragnar-lothbrok/ReviewGenie/blob/main/PRIVACY.md -->
# ReviewGenie ‚Äî Privacy Policy

**Effective date:** 2026-10-30
**Extension:** ReviewGenie ‚Äì AI Code Review, Doc & Ticket Review, Jira Ticket Generator
**Contact:** `raghunitb@gmail.com`

ReviewGenie is a "Bring Your Own Key" (BYOK) Chrome extension that reviews the documents, tickets and pull requests you open in your browser, using the AI provider **you** configure. We ‚Äî the publisher of ReviewGenie ‚Äî do **not** operate a backend, do **not** run analytics, and do **not** receive any of your data.

This policy explains exactly what data the extension touches, where it goes, and why each Chrome permission is requested.

---

## 1. Data we collect about you

**None.** ReviewGenie has no servers, no telemetry, no analytics SDKs, no advertising identifiers, no crash reporters, and no third-party trackers. The publisher cannot see your documents, tickets, code, API key, configuration, or usage.

## 2. Data stored locally on your device

The following items are stored with Chrome's `chrome.storage` API on your machine. They never leave it except as described in Section 3.

| Item | Purpose |
| --- | --- |
| AI provider, base URL, deployment name, API version, model, API type, temperature, max tokens | Routes and configures calls to your provider |
| **Your API key** | Authenticates calls to **your** AI provider |
| Display and panel settings (font size, panel scope, analysis state mode) | Remembers how you like the side panel |
| Allowed Sites list (optional) | Limits which sites ReviewGenie runs on |
| Code review team guidelines (optional) | Added to your pull request reviews |
| Last analysis of a page (its text and the AI results), per tab if you choose | Lets you reopen results without re-sending the page |
| Constraints you lock in chat | Keeps your stated rules for later chat turns |
| Chat thread ID (session storage, cleared when Chrome closes) | Continues a Responses API conversation |

Ticket and pull request reviews are kept only in the open side panel and are discarded when you close it.

Use the **Clear all** (trash) button in the side panel to delete saved analyses and constraints. Uninstalling the extension removes everything above.

## 3. Data sent to third parties

Data is sent **only when you click an action**, and only to the AI endpoint **you** configured. The actions are: Analyze Page, Ticket Review, PR Review, Requirements, Architecture Review, Security Scan, API Review, Jira Tickets, Test Plan, Capacity, Runbook, Learnings, Diagrams, Dependency Map, Data Strategy, Alternatives, Optimize Doc, Animate Diagram, and Chat.

Depending on the action, the request contains:

- **Analyze Page and document modules:** the text of the active tab (truncated to ~20,000 characters).
- **Ticket Review:** the text of the ticket page you are viewing (e.g. a Jira, GitHub, Linear or Azure Boards issue).
- **PR Review:** the code diff of the files **you select** on the pull request page, the PR title and description, and your team guidelines if you set any.
- **Chat:** your message, plus the document text and previous results (analysis, ticket review, PR review) so the AI has context.
- **Your API key**, in the header your provider expects (`Authorization`, `api-key` or `x-api-key`).

Recipients depend entirely on your settings:

- **OpenAI** ‚Üí `https://api.openai.com/v1/...` (subject to [OpenAI's privacy policy](https://openai.com/policies/privacy-policy))
- **Anthropic** ‚Üí `https://api.anthropic.com/...` (subject to [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy))
- **Azure OpenAI** ‚Üí your tenant endpoint at `*.azure-api.net` / `*.openai.azure.com` (subject to your Microsoft agreement)
- **Custom Endpoint** ‚Üí the URL you entered, such as a company gateway or a model running on your own machine (subject to that operator's terms)

ReviewGenie does **not** proxy these requests; they go directly from your browser to your provider. Whether your provider retains or trains on this data is governed by **your provider's** terms and your account settings.

When the **Responses API** mode is selected, requests are sent with `store: true` so the provider can keep the chat thread. The provider retains those responses under its own data-retention policy.

## 4. Page access

Documents, tickets and code live on many domains, so the content script loads on http(s) and file pages. On load it only adds a small floating ReviewGenie button; it does not read the page. ReviewGenie reads a page **only when you click an action**, and only the active tab.

- It reads what is **rendered on screen**. It does not call Jira, GitHub or GitLab APIs, and it never creates, edits or comments on tickets or pull requests. Findings and ticket text are copied to your clipboard for you to paste.
- It does not read pages in the background or crawl other pages.
- The only action that changes a page is **Insert into Page Editor** (Optimize tab). It asks for confirmation first and only edits the open editor.
- You can restrict ReviewGenie to specific sites in **Settings ‚Üí Allowed Sites**.

## 5. Permissions justification

| Permission | Why it is needed |
| --- | --- |
| `activeTab` | Read the current page when you click an action. |
| `storage` | Keep your settings, API key and saved results on your device. |
| `sidePanel` | Show results in Chrome's side panel. |
| `tabs` | Open the side panel and find the active tab you asked to review. |
| `contextMenus` | Provide the right-click "Analyze with ReviewGenie" entry. |
| `scripting` | Read the active page's text, ticket or code diff when you click an action. |
| `host_permissions` for `*.atlassian.net`, `*.atlassian.com` | Read Confluence and Jira pages you choose to review. |
| `host_permissions` for `*.openai.com`, `*.anthropic.com`, `*.azure-api.net`, `*.azure.com` | Call your selected AI provider directly. |
| `<all_urls>` | Review pages on any site (docs, GitHub, GitLab, internal tools) when you click an action, and reach a user-configured **Custom Endpoint**. The extension only sends data to the AI endpoint you save in Settings. |

## 6. What we do not do

- We do **not** sell, rent, or share any data.
- ReviewGenie does **not** use your documents, tickets, code or prompts to train any model.
- We do **not** include analytics, A/B testing, or fingerprinting libraries.
- We do **not** read browsing history or any tab other than the one you ask it to review.
- We do **not** send anything automatically ‚Äî every network call requires an explicit user action.

## 7. Security

- Your API key is stored in `chrome.storage.local`, isolated to the extension's origin, and is sent only to the provider you configured.
- Calls to OpenAI, Anthropic and Azure use HTTPS. A custom endpoint uses exactly the URL you enter (for example `http://localhost` for a local model).
- No remote code is loaded; all scripts ship inside the extension. Generated diagram animations run in an isolated sandbox page with no access to your stored data or to extension APIs.

## 8. Children's privacy

ReviewGenie is a developer productivity tool not directed to children under 13 and does not knowingly collect data from them.

## 9. Changes to this policy

Material changes will be reflected by updating the "Effective date" at the top and noted in the extension's release notes on the Chrome Web Store listing.

## 10. Contact

For questions or data requests: `raghunitb@gmail.com`
