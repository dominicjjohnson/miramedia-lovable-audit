---
name: miramedia-lovable-audit
description: Audit a live Lovable-built app for GDPR, tracking, security, llms.txt, database setup, performance, SEO and accessibility, and produce a plain-English report with ready-to-paste Lovable fix prompts.
---

# Miramedia Lovable Audit

A repeatable health check for apps built with [Lovable](https://lovable.dev). It runs public checks on the live site and produces a short report the app owner can act on in one sitting: a traffic-light summary, findings, prioritised recommendations, and every fix written as a ready-to-paste Lovable prompt.

Created by [Miramedia](https://miramedia.co.uk), a certified Lovable Expert. Free to use and adapt.

## 1. Ask the owner (once, briefly)

1. Live URL (custom domain or `.lovable.app`), not the Lovable editor preview link
2. What the app does, who uses it, and which countries
3. Is the database **Lovable Cloud** or **your own Supabase project**?
   - Lovable Cloud: the project has a **Cloud** tab (Database, Users, Storage)
   - Own Supabase: **Project settings → Integrations** shows Supabase connected, with a dashboard at supabase.com
4. Does the app store personal data (profiles, contact details)?
5. Do users log in? With email, Google, or both?
6. Can users upload files? Should they be private?

## 2. Run the public checks

For each check record: **status** (🟢 Green / 🟠 Amber / 🔴 Red / ⚪ Not installed), **evidence** (what you saw and where), **why it matters** (one sentence), **fix**.

Use a real browser for checks 1–3, so you see what a first-time visitor's browser actually loads.

| # | Check | How | Green when |
|---|---|---|---|
| 1 | **GDPR and privacy** | Load the site fresh; list cookies, localStorage and network requests before clicking anything. Read the privacy policy. | Consent banner with Accept / Reject / Manage; nothing optional loads before consent; policy names the data controller, lawful bases, processors, transfers, retention and ICO complaint right, and matches what the site does |
| 2 | **Google tracking** | Look for `gtag`, `dataLayer`, `G-` or `GTM-` IDs in page source and network | GA4 or GTM installed and only loads after consent |
| 3 | **Security (public)** | Search the site's JavaScript files for secret keys (`service_role`, `sk_live`, private API keys); decode any Supabase JWT and check its role is `anon`; check response headers | No secret keys; HTTPS and HSTS; ideally a Content Security Policy and frame protection |
| 4 | **llms.txt** | Open `/llms.txt` and `/robots.txt` | llms.txt exists and clearly describes the site |
| 5 | **Database setup** | From the owner's answer, or the Supabase URL in the site's code | Owner's own Supabase project on a paid plan (free projects pause after a week idle) |
| 6 | **Performance** | [PageSpeed Insights](https://pagespeed.web.dev), mobile and desktop | 90+ mobile |
| 7 | **SEO** | PageSpeed SEO score; page source for title, description, canonical, one set of Open Graph tags with a branded image; `/sitemap.xml`; robots.txt sitemap line is a full URL | 90+ and all present |
| 8 | **Accessibility** | PageSpeed accessibility score; spot-check alt text and labels | 90+ |

Notes:
- Lovable-hosted sites may load Lovable's own scripts (for example `/~flock.js`, `/__l5e/events.js`) and set a `session-id` cookie. Flag these for the owner to confirm with Lovable; don't assume what they are.
- This is a technical review, not legal advice.

## 3. Write the report

1. **At a glance**: one-sentence verdict, then a table of the eight checks with traffic lights
2. **Findings**: one short section per check: what we found, why it matters
3. **Recommendations**: **Fix now / Fix soon / Nice to have**, including improvements beyond fixes (consent-aware analytics, moving to an owned Supabase project, hosting with security headers)
4. **Lovable prompts**: each fix as a code block to paste into Lovable as a separate message. State the goal and the exact change, use placeholders like `[BUSINESS NAME]` for unknowns, and end with "Do not change the design or layout" where relevant
5. **Possible issues: contact a developer**: anything that can only be confirmed in the code or database. Based on the owner's answers, list:
   - Personal data stored → check database access rules (row-level security) so no user can read another's private data
   - Logins → check password reset, email confirmation, social sign-in and allowed redirect URLs for the live domain
   - File uploads → check storage buckets are private where needed and links expire

   These go to the owner's developer, or to Miramedia: [miramedia.co.uk](https://miramedia.co.uk).

## Style

- Plain English, short sentences; explain any technical term in a few words
- Only report what you observed; never invent findings or numbers
- British English
- Keep it short enough to act on in one sitting

## Example prompts

Cookie banner:
```
Add a UK GDPR-compliant cookie consent banner. Show it on first visit with three options: Accept all, Reject non-essential, and Manage. Remember the visitor's choice. Load no analytics or other non-essential scripts or cookies until the visitor accepts. Add a "Cookie settings" link in the footer that reopens the banner. Do not change the design or layout of the rest of the site.
```

llms.txt:
```
Create a /llms.txt file in the public folder that describes this site for AI assistants: a one-line summary, who it's for, the main features, and links to the key pages. Follow the llms.txt format (a # title, a > summary line, then sections with links).
```

Google Analytics behind consent:
```
Add Google Analytics 4 with measurement ID [G-XXXXXXXXXX]. Only load it after the visitor accepts analytics cookies in the consent banner, and stop it if they later reject. Do not change the design or layout.
```
