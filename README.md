# Portfolio

A collection of projects highlighting my work in automation, AI, and WordPress development.

---

## Automated Business Development Pipeline

**Marketing engineering in practice: a production system that turns "a company just posted a
job" into a qualified, contactable, correctly-routed lead with ready-to-send outreach,
before the sales team logs in each morning.**

This is one of the growth-marketing systems I have designed and shipped end to end. As a
full-stack marketer, I do not just plan the funnel, I build the infrastructure that fills it.

### The Problem

At a staffing and recruiting firm, business development depends on reaching the right hiring
manager at the right company at the right moment, ideally right after they post a role the
firm could fill. Done manually, that is slow and leaky: someone has to monitor job boards,
work out who owns the hire, find their contact details, and hand it to the right account
manager before the lead goes cold. I set out to automate the entire path from job posting to
warm, ready-to-send outreach sitting in the right rep's queue.

### What I Built

An end-to-end pipeline that runs every morning before the team logs in:

- **Job discovery.** Aggregates fresh postings across target markets and roles, then filters
  out staffing competitors, government listings, duplicates, and stale or re-dated postings.
- **Relevance and categorization.** Uses an LLM to read full job descriptions, decide whether
  each posting is a genuine fit, and classify it by discipline so it routes to the right
  specialist.
- **Contact discovery.** Enriches each qualified company to identify likely hiring
  decision-makers, validates them, and reveals verified contact details on demand to control
  per-lead cost.
- **Intelligent routing.** Assigns each lead to the correct account manager using territory
  rules, category specialization, load balancing, and out-of-office handling, with automatic
  re-routing and escalation when a lead sits untouched.
- **Account manager dashboard.** A custom web app where each rep sees their leads, sends
  personalized email and LinkedIn outreach in one click, logs responses, and tracks follow-up
  cycles.
- **Lifecycle marketing automation.** A daily briefing email, multi-stage follow-up reminder
  cycles, a library of conversion-tested outreach templates, and a website visit tracker that
  alerts a rep when a contact returns to the site, a strong intent signal.

### Where the Marketing Engineering Shows Up

- **Funnel thinking, in code.** The whole system is a funnel: discovery, qualification,
  enrichment, routing, outreach, follow-up, intent tracking. I built and instrumented each
  stage and rebuilt the analytics so reporting reflects real rep activity and true conversion
  between stages.
- **Messaging and conversion.** I wrote the outreach sequences, structured them as a staged
  journey from first touch to breakup email, and built LLM-assisted drafting so reps send
  personalized, on-brand messages without starting from scratch.
- **Attribution and intent.** The visit tracker ties website behavior back to specific
  contacts so reps can act on buying signals, with filtering to screen out automated and
  bot traffic so the signal stays clean.
- **Lifecycle automation.** Reminder cycles, escalation logic, and the morning briefing keep
  leads moving and stop them going stale, without anyone having to babysit the process.

### Tech Stack

**Languages & Runtime**
- Node.js (22.x), JavaScript, HTML, CSS
- No framework, hand-built for a lean serverless footprint

**Infrastructure & Hosting**
- Vercel (serverless functions, production deploys via Git integration)
- Upstash Redis (primary datastore, caching, deduplication, and state)
- cron-job.org (external scheduler driving the daily pipeline and recurring jobs)

**AI & Data Enrichment**
- Google Gemini (LLM for job-relevance classification, category detection, contact
  validation, domain inference, and personalized email/LinkedIn message drafting, with
  automatic API-key failover)
- Apollo.io (B2B contact discovery and verified email enrichment)
- JSearch via RapidAPI (job posting aggregation across major job boards)
- Brandfetch (company logo resolution by domain)

**Email, CRM & Outreach**
- Nodemailer over Gmail SMTP (transactional and briefing emails)
- Mailchimp (contact records, merge-field personalization, rep assignment, visit tracking IDs)
- HMAC-token unsubscribe/opt-out flow for compliance

**Front End**
- Custom single-file dashboard (vanilla JS, no framework) with live lead management,
  one-click outreach composer, response logging, analytics funnel, and team leaderboard
- WordPress / Elementor integration for the website visit tracker (interaction-gated
  JavaScript beacon)

**Engineering Practices**
- Git / GitHub version control with command-line deploy workflow
- Staggered batch processing to stay within serverless execution-time limits
- Multi-stage filtering and deduplication chain
- API cost control through on-demand enrichment and response caching

### Outcome

What was a manual, inconsistent prospecting process is now an automated pipeline that does the
groundwork overnight. The team starts each day with qualified, contactable, correctly-routed
leads and outreach ready to send. It runs on its own and keeps improving as I tune it against
real response data, which is the part I enjoy most: treating the whole go-to-market motion as
a system I can measure and optimize.

> 🔒 *Built for iMPact Business Group. Source code lives on the company GitHub account.*

---

## Impact Web Search — Custom WordPress Job Search Plugin

A WordPress plugin that connects a staffing company's website to its live job feed, letting visitors search openings directly from any landing page without leaving the site.

### The Problem

Our public job board lived on a separate subdomain. Visitors landing on marketing pages had no quick way to search openings without navigating away, and the board's native search only matched job titles, missing relevant roles when someone searched by skill or keyword.

### What I Built

A self-contained WordPress plugin (PHP, vanilla JavaScript, CSS) that ingests the company's XML job feed, caches it, and exposes two shortcodes that drop into any page or page-builder widget:

- **A search widget** with type-ahead autocomplete that matches against job title, location, reference number, and full job description, so a search for "SQL" surfaces a Database Administrator role even when the title never mentions it. Multi-keyword searches use AND logic across all fields. Results link directly to the relevant posting.
- **A recent jobs module** that displays the newest openings filtered by category and count, configurable through an admin UI where non-technical users create and manage reusable shortcode presets without touching code.

### Technical Highlights

- Hourly feed caching via WordPress transients and WP-Cron to keep page loads fast and avoid hammering the source feed
- Client-side autocomplete that filters a localized data payload, no per-keystroke server round-trips
- Per-surface click tracking that integrates with the job board's analytics, so the marketing team can see exactly where applicant traffic originates
- Built following WordPress security best practices: input sanitization, output escaping, capability checks, nonce-protected forms, and a unique prefix throughout
- Fluid, responsive layout that adapts to desktop and mobile and inherits the host page's container width

### Stack

PHP, JavaScript, CSS, WordPress Plugin API (Shortcodes, Settings API, Transients, WP-Cron), XML feed parsing

> 🔒 *Built for iMPact Business Group. Source code lives on the company GitHub account.*
