# Miramedia Lovable Audit

A free, open checklist and AI skill for auditing apps built with [Lovable](https://lovable.dev).

It checks a live Lovable app for the things that usually get missed between "it works" and "it's ready": privacy and cookies, analytics, security, `llms.txt`, database setup, speed, SEO and accessibility. The output is a plain-English report with traffic-light ratings, prioritised recommendations, and every fix written as a prompt you can paste straight into Lovable.

## What it checks

| Check | What it looks for |
|---|---|
| GDPR and privacy | Cookie consent, what loads before consent, privacy policy completeness |
| Google tracking | GA4 or Tag Manager, and whether it waits for consent |
| Security | Exposed secret keys, HTTPS and security headers |
| llms.txt | Whether AI assistants have a guide to your site |
| Database setup | Lovable Cloud or your own Supabase project |
| Performance | PageSpeed mobile and desktop scores |
| SEO | Titles, descriptions, social sharing tags, sitemap, robots.txt |
| Accessibility | PageSpeed accessibility score, alt text, labels |

## How to use it

**With Claude:** add [`Miramedia_Lovable_Audit.md`](Miramedia_Lovable_Audit.md) as a skill, then ask Claude to audit your app's live URL.

**By hand:** follow the checklist in the file. Each check says how to test it and what "good" looks like.

## What it doesn't cover

Some things can only be checked in your app's code and database, such as whether users can see each other's data, how logins are configured, and whether uploaded files are private. The report lists these as possible issues for your developer to check.

## Need help?

Built by [Miramedia](https://miramedia.co.uk), a UK web consultancy and certified Lovable Expert with 20+ years of building for media and events brands. We can run the audit for you, make the fixes, move your app to hosting and a database you own, and look after it afterwards.

Contact: [miramedia.co.uk](https://miramedia.co.uk)

## Licence

Free to use and adapt. A credit to Miramedia is appreciated.
