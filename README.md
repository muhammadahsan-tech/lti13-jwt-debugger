<img width="1440" height="779" alt="Screenshot 2026-05-11 at 6 15 00 PM" src="https://github.com/user-attachments/assets/0c0ae1e2-00df-4c36-a52d-68a178993502" />

# 🔍 LTI 1.3 JWT Debugger

> A free, browser-based tool to decode, inspect, and validate LTI 1.3 JWT tokens (id_token) — no backend, no login, no data sent anywhere.

**🚀 Live Tool → [muhammadahsan-tech.github.io/lti13-jwt-debugger](https://muhammadahsan-tech.github.io/lti13-jwt-debugger)**

Built by [Muhammad Ahsan](https://github.com/muhammadahsan-tech) — LTI 1.3 architect who has implemented the spec from both sides: as a platform (LMS) and as a tool provider.

---

## What It Does

Paste any LTI 1.3 `id_token` JWT and instantly get:

- **Decoded Claims** — organized into JWT Header, Standard OIDC Claims, LTI 1.3 Claims, and LTI Advantage Services sections
- **Plain-English explanations** — every claim has a description of what it means and why it matters
- **Validation** — 20+ checks against the LTI 1.3 spec including required claims, algorithm, expiry, message type, AGS/NRPS/Deep Linking presence
- **Raw JSON** — clean formatted header and payload with copy buttons
- **Auto-decode on paste** — no button click needed, decodes the moment you paste

---

## Screenshot

```
┌─────────────────────────────────────────────────────────────┐
│  LTI 1.3  JWT Debugger                    by Muhammad Ahsan │
├──────────────────────────────────────────────────────────────┤
│  INPUT — ID_TOKEN JWT    │  CLAIMS  VALIDATION  RAW JSON    │
│                          │                                   │
│  eyJhbGci...             │  ▼ JWT HEADER          (2)       │
│                          │  ▼ STANDARD CLAIMS     (6)       │
│                          │  ▼ LTI 1.3 CLAIMS      (8)       │
│                          │  ▼ LTI ADVANTAGE        (2)       │
│  ● VALID                 │  ✓ 18 passed  ⚠ 1 warning       │
└──────────────────────────────────────────────────────────────┘
```

---

## Who This Is For

- **Developers** building LTI 1.3 tool providers — debug launch failures without digging through server logs
- **LMS administrators** — inspect what Canvas, Moodle, or Blackboard is actually sending your tool
- **EdTech architects** — validate JWT structure against the LTI 1.3 spec before going to production
- **QA engineers** — verify all required claims are present and correctly formed

---

## Validation Checks

The debugger runs the following checks automatically:

| Check | What it validates |
|---|---|
| Algorithm | RS256 or RSA variant (symmetric algorithms flagged) |
| Required claims | All 11 LTI 1.3 required claims present |
| Token expiry | `exp` claim checked against current time |
| Token lifetime | Flags tokens with unusually long expiry windows |
| LTI version | Must be `1.3.0` |
| Message type | `LtiResourceLinkRequest`, `LtiDeepLinkingRequest`, or `LtiSubmissionReviewRequest` |
| Issuer | Canvas, Moodle, or custom issuer detected and labeled |
| Roles | Roles present and parsed |
| AGS endpoint | Assignment & Grade Services endpoint and scopes |
| NRPS endpoint | Names & Role Provisioning Service endpoint |
| Deep Linking | Settings and `deep_link_return_url` validated for DL launches |

---

## Claims Reference

The debugger explains every standard LTI 1.3 claim in plain English:

| Claim | Explained as |
|---|---|
| `iss` | The LMS platform issuing this JWT |
| `sub` | Unique identifier for the user within the platform |
| `aud` | Your tool's Client ID — must match what's in the LMS |
| `iat` / `exp` | Issued at / expires at — shown as human-readable timestamps |
| `nonce` | One-time value — must be validated and never reused |
| `message_type` | LtiResourceLinkRequest vs LtiDeepLinkingRequest |
| `deployment_id` | Which deployment of the tool is launching |
| `target_link_uri` | Where the tool should redirect after JWT validation |
| `context` | Course information — id, label, title |
| `roles` | User's LTI roles — Learner, Instructor, Administrator |
| `resource_link` | The specific link that was clicked |
| AGS endpoint | Grade passback URL and available scopes |
| NRPS endpoint | Course roster fetch URL |
| Deep Linking settings | Content return URL and accepted content types |

---

## Privacy

**100% client-side.** Your JWT never leaves your browser. There is no backend, no analytics on JWT content, no logging. The tool runs entirely in the browser using vanilla JavaScript.

---

## Running Locally

No build step needed — it's a single HTML file.

```bash
git clone https://github.com/muhammadahsan-tech/lti13-jwt-debugger.git
cd lti13-jwt-debugger
open index.html
```

Or serve it locally:

```bash
npx serve .
# or
python3 -m http.server 8080
```

---

## Common LTI 1.3 Launch Errors This Tool Helps Debug

**"Invalid nonce"**
The nonce in the JWT doesn't match what your tool stored during the OIDC login step. Check that your tool is storing the nonce server-side before redirecting to the LMS.

**"JWT expired"**
The `exp` claim is in the past. JWTs must be validated immediately on receipt — do not cache or reuse them. The debugger shows exactly when the token expired.

**"Missing required claim: deployment_id"**
The LMS is not sending the deployment ID. Check that your Developer Key is fully configured and the tool is deployed to the correct account or course.

**"Algorithm is HS256"**
LTI 1.3 requires asymmetric signing (RS256). A symmetric algorithm means the JWT was not generated by a compliant LMS — likely a test or misconfigured tool.

**"Missing message_type"**
The JWT is missing the LTI message type claim. This is required by the spec and indicates a non-compliant LMS or a malformed test token.

---

## Related Repositories

- [lti13-multilms-tool](https://github.com/muhammadahsan-tech/lti13-multilms-tool) — Working LTI 1.3 tool provider compatible with Canvas, Moodle, and Blackboard
- [lti13-canvas-integration-guide](https://github.com/muhammadahsan-tech/lti13-canvas-integration-guide) — Step-by-step Canvas LTI 1.3 integration guide with code examples
- [awesome-lti13](https://github.com/muhammadahsan-tech/awesome-lti13) — Curated list of LTI 1.3 libraries, tools, and resources

---

## About the Author

**Muhammad Ahsan** is a Lead Software Engineer and LTI 1.3 architect with hands-on experience on both sides of the LTI handshake:

- **Platform side:** Architected LTI 1.3 compliance for a proprietary higher education LMS at Perdoceo Education Corporation, enabling integration with third-party edtech vendors across AGS, Deep Linking, NRPS, and Submission Review
- **Tool side:** Designed and built an independent LTI 1.3 Tool Provider compatible with Canvas, Moodle, and Blackboard

[Connect on GitHub →](https://github.com/muhammadahsan-tech)

---

## Contributing

Found a bug or want to add a validation check? Pull requests are welcome.

1. Fork the repo
2. Make your changes to `index.html`
3. Test with a real LTI 1.3 JWT or the built-in sample
4. Open a pull request

---

*If this tool saved you debugging time, consider starring the repo ⭐ — it helps other developers find it.*
