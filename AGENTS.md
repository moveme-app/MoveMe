# AGENTS.md: rules for AI coding assistants working on Move Me

Read this before changing anything. It applies to every tool (Codex, Claude, others) and every teammate using one.
Product details live in `README.md` and `PRD.md`; this file is about **how to work on the code safely**.

## Project in one paragraph
Move Me (https://www.move-me.co) is a moving planner and service marketplace for the Dallas, Houston and Austin metros. It has three roles: customer, provider and admin. The whole front end is **one file, `index.html`**, hosted on GitHub Pages from `moveme-app/MoveMe`. The backend is the Supabase project **Move Me** (Postgres, Auth, Storage). There is no build step.

## 1. Always start from the latest code
- The **only source of truth is the current `index.html` in this repository.** Before editing, get the latest copy from the repo.
- **Never** rebuild from an older copy, an attachment, or a file with another name (for example `MoveMe_1.html` or `MoveMe_3.html`). Doing that has erased features before.
- If you're given a file that differs from the repo, **compare them first** and list what would be added or lost before replacing anything.
- After a change, the file to upload is still named exactly `index.html`.

## 2. How `index.html` is structured
- The base app comes first. Later features are added as **override blocks** that wrap earlier functions, for example `const prev = renderPlan; renderPlan = function(...a){ prev(...a); /* extra */ };`.
- **Add new behavior the same way.** Put a new block, or a new `<script id="...">` near the end, that wraps the existing function. Don't rewrite or delete earlier blocks.
- Screens are registered with `navWrap(name, fn)` and the `SCREENS` map. New screens must be registered there, and in `screenAllowed()` if they need someone signed in.
- The Supabase JS library is bundled inline in `<script id="supabase-sdk">`. **Don't edit it.**
- Config constants: `SUPABASE_URL` and `SUPABASE_KEY` (the publishable key, which is safe to be public), and `MOVEME_GEOAPIFY_KEY` for address search.
- Keep everything in one file. **Don't add frameworks, a build step or extra JS/CSS files** unless the team agrees.

## 3. Files that must stay in the repo
| File | Rule |
|---|---|
| `CNAME` | **Never delete.** It connects the repo to move-me.co. |
| `.nojekyll`, `.well-known/assetlinks.json` | Keep. The Android app needs them to open full screen. |
| `manifest.webmanifest`, `sw.js`, `icon-*.png`, `apple-touch-icon.png`, `favicon-32.png` | Keep. They make the site installable as an app. |
| `Move_Me.apk` | Keep the exact name; the landing page links to it. |

## 4. Database rules (Supabase)
- **Additive changes only.** Never `DROP` or `TRUNCATE` tables, columns or functions, or delete data, without explicit approval from the project owner. To change a function's shape, create a new version (for example `_v4`) and point the app at it.
- The app uses these **current booking functions**: `moveme_submit_requests_v3`, `moveme_customer_requests_v3`, `moveme_provider_requests_v3`, `moveme_decide_request_v3`, `moveme_cancel_request_v3`, `moveme_cancel_plan_requests_v3` and `moveme_admin_applications_v3`. Older versions without `_v3` are kept for history. Don't build on them.
- Every new function must:
  - be `SECURITY DEFINER` with `set search_path = ''`;
  - revoke execute from `public` and `anon`, and grant it to `authenticated`;
  - check who the caller is (`auth.uid()`), and check `private.is_admin()` for admin-only actions.
- Row-level security stays **on** for every table. The app should go through functions, not direct table writes. The one exception is `moveme_home_media`, which has its own policies.
- **Prices and fees are calculated on the server**, by `private.quote_v3` with a 10% fee (`commission_bps = 1000`). Never trust a price sent from the browser.
- The service tiers in `SERVICE_MODELS` (in `index.html`) must match `private.service_keys`, `private.service_extras` and `private.service_inclusions` in the database. Change both together.
- **Don't change stored values:**
  - Cities: `"Dallas, TX"`, `"Houston, TX"`, `"Austin, TX"`, `"All three cities"`.
  - Booking status: `requested`, `accepted`, `declined`, `completed`, `cancelled`.
  - Provider status: `pending`, `approved`, `rejected` (`rejected` is shown as "Paused").
  - Suburbs map to these values through `METRO_AREAS`.

## 5. Secrets: this repo is public
**Never commit** any of these:
- the Android signing key or keystore, or its password
- the admin password, or any user's password
- the Supabase service-role (secret) key or database password

Share them privately within the team.

## 6. Before you say a change is done
- Test as each role it affects: **customer, provider and admin**.
- Check at **phone width (about 390 px)** and desktop, with no errors in the browser console.
- If the database changed, test the function as a signed-in user, and check that a non-admin is blocked from admin functions.
- Say plainly what changed, which files need uploading, and anything you couldn't test.

## 7. Deploying
- Upload the changed `index.html` (and any new files) to `moveme-app/MoveMe`. GitHub Pages republishes in 1–2 minutes.
- Database changes take effect immediately and need no upload.

## 8. Writing and design
- Use plain, friendly wording that users understand. Avoid jargon such as "RPC", "tier key" or "RLS" in the interface.
- Reuse the existing CSS variables (`--navy`, `--coral`, `--ink`, `--muted`, `--line`, `--card`, `--surface`) and existing classes, so new screens match.
- Keep it accessible: label every input, use real buttons, make it keyboard-usable, and use `role="alert"` or `aria-live` for messages.

## 9. Known limits (don't "fix" these silently)
- Payments are **simulated**. Don't add real payment processing without the team deciding to.
- Supabase's built-in email only reaches project team members. Password resets for customers rely on the admin reset tool until a custom email sender (SMTP) is set up.
- The free Supabase plan pauses after about 7 days of inactivity.
