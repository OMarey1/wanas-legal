# Legal pages

The two public pages Google Play requires before Wanas can be submitted.

| File | Where it goes in the Play Console |
|---|---|
| `privacy-policy.html` | Store listing → **Privacy policy URL** |
| `delete-account.html` | App content → Data deletion → **web page to request deletion** |
| `index.html` | Landing page linking both |
| `style.css` | The app's design system, ported to the web |

Bilingual (AR/EN) with a language toggle, RTL-aware, self-contained, no build step.

## Design

`style.css` is ported from `src/theme/tokens.ts` and `src/theme/typography.ts`
rather than invented: cream `#F6F3EC` screen, white cards at `--r-lg` 18px with
the `shadows.raised` elevation, emerald `#00674A` accent, `slate`/`alert` for
secondary and urgent text, the `typeScale` sizes, and Cairo for Arabic with
Poppins for Latin — the same `fontForCurrentDirection` split the app uses,
loaded from Google Fonts. Light only, because the app is.

**If a token changes in the app, change it here too.** The point is that a
member tapping through from the app does not feel like they left it.

## Content

These describe the app as actually built — the per-doctor permission grants and
their immediate revocation, the anonymous-ID administrator surface, the
confirmation-first safety process, the three deletion blockers from migration
`117_account_deletion`, the private storage buckets and short-lived signed URLs,
and the deliberate absence of automated scoring. If that behaviour changes,
these pages change with it.

Filled-in values: controller **Omar Marey**, contact **wanas@getkensho.ai**,
payment provider **Geidea**, hosting region **Frankfurt (eu-central-1)**,
dated **24 September 2026**.

### Retention periods — confirm with a lawyer

Four numbers are stated as commitments and should be checked before launch, since
a privacy policy is binding:

| Stated | Value |
|---|---|
| General data after deletion | 30 days |
| Clinical records / session notes | 5 years from last session |
| Payment and invoice records | 5 years (Egyptian tax record-keeping) |
| Safety-case records | 5 years from resolution |
| Security audit logs | 2 years |

The clinical one is the least certain — professional standards vary, and Egypt
has no single obvious rule for private psychotherapy notes. If your advisor gives
a different figure, change it in both HTML files (English and Arabic).

Also confirm: whether the controller should be you personally or a company. It
currently says **Omar Marey**, matching a personal Play Console account.

## Hosting — GitHub Pages

The app repo is private, so Pages would need a paid plan. Publish from a separate
public repo instead; nothing here is secret.

```bash
cd legal
git init -b main
git add .
git commit -m "Wanas privacy policy and account deletion pages"
gh repo create wanas-legal --public --source=. --push
gh api -X POST repos/OMarey1/wanas-legal/pages -f 'source[branch]=main' -f 'source[path]=/'
```

Live a minute or two later at:

- `https://omarey1.github.io/wanas-legal/privacy-policy.html`
- `https://omarey1.github.io/wanas-legal/delete-account.html`

To update afterwards: edit the files here, then `git add -A && git commit && git push`
from the `legal/` folder.

### A custom domain, later

If you point `wanas.app` (or similar) at it, add a `CNAME` file containing the
domain and set the DNS records GitHub shows under Settings → Pages. Play accepts
the `github.io` URL, so this is cosmetic.

## Before you submit

- Link the privacy policy from inside the app, not only from the store listing.
- Keep the Data safety form consistent with section 2 of the policy. Google
  cross-checks the declaration against the app's real network behaviour, and a
  mismatch is a rejection.
