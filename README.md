# Move Me

**One plan for your whole move.** Move Me turns a few move details into a personalized moving plan: a timeline, a checklist, upfront costs, and local providers to book for every task. Customers, service providers and an administrator each have their own side of the app.

- **Live site:** https://www.move-me.co
- **Repository:** `moveme-app/MoveMe` (GitHub Pages)
- **Backend:** Supabase project **Move Me**
- **Team:** Team 4PM: Aakanksha Khare, Arshia Hussain, Ethan Varghese, Samuel Arogundade
- **Service area:** the Dallas, Houston and Austin metro areas, including suburbs (Plano, Katy, Round Rock and so on)

---

## What the app does

### Customers
- Create an account and describe the move: both home addresses (with address search), move date, home size, stairs or elevator access, and service needs (box range, cleaning level, internet or utility setup, handyman hours, storage unit size, junk load).
- Get a move plan with a timeline, a to-do list, due dates and a running cost total.
- Compare 2 or more providers per service with prices calculated for *their* move, ratings, inclusions and availability.
- Book a provider by choosing an open date and time slot (8 am–noon or noon–5 pm). Bookings confirm instantly.
- Upload home photos (up to 6) and a walkthrough video (1), and share them with booked providers.
- Cancel bookings, choose a replacement if a provider cancels, rate completed services, and report a service issue.
- Look back at past moves and change their password.

### Providers
- Create an account, then complete a 3-part business setup: **Business and services**, **Prices and inclusions**, **Availability and contact**.
- The listing goes live automatically once setup is complete and the email address is confirmed. No manual approval is needed.
- Manage bookings: view job details (addresses, requirements, home media), mark jobs complete, or cancel with a reason.
- Availability calendar: block dates or pause new bookings.
- Earnings and payouts: the customer total, Move Me's 10% fee and the provider's 90% share for every booking.

### Admin
- **Providers:** view every provider, its services and prices; pause or restore listings; view earnings.
- **Customers:** see who signed up, who built a plan and what they booked; export to CSV.
- **Booking issues:** review and resolve reported service problems.
- **Payouts:** see fees earned, pending and paid payouts, and run a payout check.
- Hide or restore reviews, and reset a customer's or provider's password.

### Services offered

| Service | Priced by | Provider-set tiers |
|---|---|---|
| Movers | Home size | Studio to 4+ bedrooms, plus between-city and stairs extras |
| Packing (packers) | Box range | 1–20, 21–40, 41–60 boxes |
| Unpacking | Box range | 1–20, 21–40, 41–60 boxes |
| Packing supplies | Box bundle | 20, 40, 60 boxes |
| Utilities and internet setup | Package | Internet, utilities, both |
| Cleaning | Home size | Studio to 4+ bedrooms, plus deep-clean extra |
| Handyman and repairs | Visit length | 1, 2, 4 hours |
| Storage | Unit size, per month | 5×5, 5×10, 10×10 ft |
| Junk removal | Truck load | Quarter, half, full |

Providers set their own prices; the app suggests starting amounts. Customer prices include Move Me's 10% fee.

> **Payments are simulated.** No real money moves. A booking is recorded as *authorized*, becomes *paid* when the provider marks it complete, and is *released* if cancelled. Provider payouts are scheduled for the first Friday after completion.

---

## How it's built

| Part | Technology |
|---|---|
| Front end | One self-contained `index.html` (HTML, CSS and JavaScript; the Supabase JS library is bundled inline) |
| Hosting | GitHub Pages with a custom domain (`move-me.co`, registered with GoDaddy) |
| Database and sign-in | Supabase (Postgres, Auth, Storage) |
| Address search | Geoapify autocomplete; suburbs are matched to their metro by county |
| Mobile | Installable web app (manifest and service worker); Android APK built with PWABuilder |

### Files in this repository

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest`, `sw.js` | Make the site installable as an app |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`, `favicon-32.png` | App icons |
| `Move_Me.apk` | Android app, downloadable from the landing page |
| `.well-known/assetlinks.json` | Lets the Android app open full screen without a browser bar |
| `.nojekyll` | Makes GitHub Pages serve the `.well-known` folder |
| `CNAME` | Connects the repository to `move-me.co`; **do not delete** |

### Database (Supabase)

**Main tables**
- `customers`, `providers`: accounts created on sign-up
- `move_plans`: each customer's saved plan
- `service_requests`: bookings, with the saved price breakdown, payment and payout status
- `booking_reviews`, `booking_issues`, `provider_payouts`, `provider_blocked_dates`
- `moveme_home_media`, plus the private storage bucket `moveme-home-media`

**Security**
- Row-level security is on for every table.
- The app works through database functions (`moveme_*`), which check who is signed in.
- Admin access comes from the private `private.admins` table.

Older function versions are kept for history. The current app uses the `_v3` booking functions.

---

## Deploying changes

1. Edit `index.html`. Always start from the latest copy in this repository.
2. In GitHub: **Add file → Upload files**, replace `index.html`, then **Commit**.
3. GitHub Pages republishes in 1–2 minutes. Hard-refresh to see it (Ctrl + Shift + R, or Cmd + Shift + R on a Mac).

Database changes are made in Supabase and take effect immediately, without an upload.

## Installing the app
- **iPhone:** open move-me.co in Safari, tap **Share**, then **Add to Home Screen**.
- **Android:** tap **Download for Android** on the landing page, then open the file to install. The phone will ask to allow the install.

---

## Operating notes and known limitations

- **Supabase free plan pauses after about a week with no activity.** Sign in at least weekly, especially before a demo.
- **Email:** Supabase's built-in email only reaches project team members (2 emails per hour), so customers don't get reset or confirmation emails. Until a custom email sender is connected (Brevo or Resend, with `noreply@move-me.co`), admins reset passwords from the portal and users change them under **Account → Change password**.
- **No notifications:** there are no emails or texts about bookings yet. Everything appears inside the app.
- **Payments are simulated:** there's no card processing.
- **iOS has no App Store version** (that needs a Mac and a $99/year Apple account). **Android isn't on Google Play** (that's $25 one-time). The Android signing key is kept outside this repository.
- **Supabase's free plan has no read-only team role.** Teammates can be Developers at most.

## Accounts
- **Admin:** `admin@move-me.co`. Share the password privately, never in this file or the repository.
- Demo providers and the demo customer were removed on Oct 27, 2026. Live providers sign up through the app.
