# MatchMentum Changelog

All notable changes to MatchMentum are documented here.  
Format: **Added** (new features) | **Changed** (modifications to existing) | **Fixed** (bug fixes) | **Removed** (deleted functionality)

Hotfixes ship immediately as patch releases (e.g. v1.0.1) outside the regular bi-weekly cycle.  
Scheduled releases ship every two weeks on Saturdays.

---

## [Unreleased] — v1.2.0 · Target: 2026-04-11

> Items logged here since last release. Move to a versioned section on release day.

---

## [v1.1.0] — 2026-03-28 · Gap Context Modal + Background Context Routing

### Added
- Gap context guided modal: replaces freeform textarea with Claude-generated questions based on gaps identified in the job analysis (capped at 4 questions)
- Questions are specific to the gaps in the user's resume vs. the job description — not generic
- Optional When and Role/context fields per question
- Confirmation screen shows plain-language summary of what will be added to profile before saving
- Pill indicator appears after confirming: "✓ Background Context updated"
- Background Context field added to profile review screen below Certifications — editable, persists to cloud
- Staging environment: matchmentum-staging.netlify.app deployed from staging branch, auto-deploys on push

### Changed
- Gap answers now write to dedicated `profileData.backgroundContext` field (previously appended to `profileData.experience` where they were silently ignored)
- Background context accumulates across modal submissions — does not overwrite
- `confirmProfile()` explicitly includes `backgroundContext` in profile rebuild to prevent silent data loss on save
- Beta tier now displays correctly in sidebar: badge shows "Beta", upgrade link hidden, usage bars show unlimited
- Scheduled release cadence updated from Wednesdays to Saturdays

### Fixed
- Background context now injects into all 4 generation prompts (Chunk 1 summary, Chunk 2 recent experience, Chunk 3 older experience, cover letter) with candidate-confirmed trust signal
- Dead `TIER_LIMITS.trial` reference removed from `getUserSubscription()` — was causing new user onboarding to fail with "Cannot read properties of undefined" error
- Upgrade modal no longer displays "null job analyses" — null limits now render as "Unlimited"
- Beta tier accounts now correctly show unlimited usage in sidebar and account modal

### Database
- All beta tester subscription rows updated: `resumes_limit`, `covers_limit`, `analyses_limit` set to null (unlimited)
- Staging test account (`charisselenee@icloud.com`) added as beta tier for staging testing
- Staging URL (`https://matchmentum-staging.netlify.app`) added to Supabase Auth redirect URL allowlist

---

## [v1.0.0] — 2026-02-16 · Initial Production Launch

### Added
- Core resume analysis flow: upload resume + paste job description → AI-generated match analysis
- Resume generation: tailored resume output from profile + job description
- Cover letter generation with AI-generated content
- Resume Readiness Score with rubric-based evaluation (required quals 80 pts, preferred quals 20 pts, partial credit tiers)
- Score breakdown: per-category feedback (keywords, format, structure, quantification)
- Three-tier subscription model: Free, Lite ($14.99/mo), Pro ($29.99/mo)
- Usage tracking and enforcement: `checkUsageLimit()` → process → `incrementUsage()`
- Stripe integration: checkout sessions, billing portal, webhooks for subscription sync
- Supabase auth: email/password + Google OAuth
- Email verification requirement on signup
- Row-level security on all database tables (user_profiles, user_documents, subscriptions)
- Cloud sync: profile and generated documents persist across devices
- DOCX export for generated resumes and cover letters
- Toast notification system replacing all browser `alert()` dialogs
- Loading states throughout generation flow
- XSS protection via `escapeHtml()` (22+ call sites)
- Analytics framework (stub, pending provider decision)
- Landing page with full marketing sections visible to anonymous visitors
- Auth gate for unauthenticated users with blurred app backdrop
- Terms of Service and Privacy Policy pages (GDPR/CCPA compliant)
- Marketing opt-in checkbox on signup (unchecked by default)
- Terms acceptance timestamp stored on user_profiles

### Architecture
- GitHub Pages (static frontend) + Netlify (serverless functions) split architecture
- Four Netlify function endpoints: `claude-proxy`, `create-checkout-session`, `generate-resume-docx`, `create-portal-session`
- Supabase PostgreSQL with RLS; database trigger creates user_profiles row on new signup

---

## [v1.0.1] — 2026-02-17 · Hotfix: Free Tier Correction

### Changed
- Free tier resume generations: 0 → 1 (1 resume generation included, DOCX export bundled)
- Pricing card updated to reflect 1 resume generation with checkmark
- DOCX export row removed from free tier pricing card (now implied by the 1 generation)
- `actionLabels` updated from "resume generations" → "resume generation" (singular)
- `terms.html` free tier description updated to match

---

## [v1.0.2] — 2026-02-17 · Hotfix: Database Trigger + Backfill

### Fixed
- Added Supabase trigger to auto-create `user_profiles` row on new user signup (previously missing, caused auth edge cases)
- Backfilled `user_profiles` rows for all existing users

---

## Post-Launch Improvements (Feb–Mar 2026)

*The following were shipped iteratively post-launch. Grouped here for reference; future work will follow the bi-weekly release schedule.*

### UI Redesign
- Dashboard redesigned: "Last Session" card surfaces most recent job (company name, Resume Readiness Score, date) with quick-action button
- Generated files display as full-width cards with metadata (filename, score, date) and inline download/delete actions
- Navigation simplified: "View Documents" removed in favor of unified "View History"
- Decorative hero section (rocket graphic, floating circles) removed from logged-in dashboard; replaced with task-focused two-column layout
- Sidebar usage widget added (shows monthly usage vs. limits by tier)

### Scoring
- Score comparison display (before/after between profile score and resume score) removed from generation flow — `reAnalyzeWithResume` function retained in codebase but not called
- Resume Readiness Score established as the primary success metric shown on result
- "ATS score" terminology retired; renamed to "Resume Readiness Score" throughout UI
- Score tooltip and explainer added: Claude-generated rubric methodology, not a direct ATS system readout
- Scoring function updated to evaluate full resume and full job description (no character truncation)

### Cover Letter
- Cover letter generation prompt comprehensively revised
- Guardrails added against AI-detectable patterns: banned opener types (subordinate clauses, first-person declaratives, mirrored JD language), banned phrases list, banned closings, banned greetings, em dash and semicolon restrictions, metrics density rules

### Brand & Copy
- Tagline updated to "Written for the job. Ready for the system." (replaced "Build Career Momentum Fast")
- Page title and meta description updated
- Landing page hero H1 updated to match tagline (replaced "Resumes tailored to every job you want")
- `MatchMentum-Week1-Graphics.html` updated with new tagline

### Tier & Subscription
- `trial` tier removed from `TIER_LIMITS` — confirmed dead code, no users assigned this tier in production
- `beta` tier added to `TIER_LIMITS` with unlimited access matching Pro — beta users excluded from MRR calculations
- `subscriptions_tier_check` constraint updated to include `beta` as a valid tier value
- 4 beta tester accounts migrated from `pro` to `beta` tier (users with no Stripe subscription ID)

---

## Under Consideration — Not Yet Decided

- Stacked wordmark variant: full two-line vs. first-line-only layout for new tagline
- URL fetching via Netlify proxy (deprioritized — major job boards block scraping; company career pages more viable)
- Elite tier feature development: weekly job matching email digest, interview prep, application tracker, skills gap analysis
- Mobile strategy: PWA, hybrid, or native app
- Analytics provider: Google Analytics or Plausible

---

*Maintained by Penelope | matchmentum.com*
