# Move Me: Product Requirements Document

| | |
|---|---|
| **Product** | Move Me, a moving planner and service marketplace |
| **Team** | Team 4PM: Aakanksha Khare (Product and Research), Arshia Hussain (Engineering and Systems), Ethan Varghese (Design and Experience), Samuel Arogundade (Business and Strategy) |
| **Status** | Live MVP at https://www.move-me.co |
| **Last updated** | November 6, 2026 |
| **Market** | Dallas, Houston and Austin metro areas, Texas |

---

## 1. Summary

Move Me turns a move into one dependable plan. A customer enters their addresses, move date, home size and service needs. Move Me builds a timeline and checklist, prices every service for that specific move, and lets the customer book local providers into open time slots, all in one place. Providers get a self-serve way to list services, set their own prices, control their availability and track earnings. An admin portal oversees providers, customers, payouts and service issues.

## 2. Problem

A move is never just "hire a mover." One move can involve movers, packing, cleaning, storage, junk removal, repairs and setting up utilities. Today people coordinate all of it across separate websites, calls and texts, with no shared timeline or budget. Tasks get missed, deadlines slip, and costs come as a surprise.

**Evidence: our survey of 45 people about what they used to plan their last move**

| Planning method | Share of respondents |
|---|---|
| A general notes app | 40% |
| A paper checklist | 38% |
| Nothing formal ("kept it in my head") | 33% |
| Text or email threads | 33% |

Most people combined two or three of these, and none of them were shared with anyone.

**The gap in existing products**
- **Updater, Moved and MoveEasy** reach people only through property managers or brokers.
- **HireAHelper and Thumbtack** cover one task at a time.
- **SIRVA and Cartus** serve corporate relocation programs.

Nobody offers a self-serve plan that covers every task, with a vetted shortlist for each one, sized for a real but modest budget.

## 3. Target users

| Segment | Description | Priority |
|---|---|---|
| **Professionals relocating for work** | Have a confirmed move date and often a $500–$3,000 relocation stipend, but no corporate relocation service. Our largest and best-validated segment. | **Primary** |
| Students, renters and young professionals | Move often and are comfortable booking online. | Secondary |
| Local service providers | Movers, packers, cleaners, storage, junk removal, handymen and utility-setup businesses in the three metros. | Supply side |
| Move Me administrators | The team operating the marketplace. | Internal |

**Persona: Maya.** She accepts a new job and her move date is set. Before Move Me she juggles notes, texts and half-remembered advice, and feels overwhelmed. With Move Me she enters her move, gets a full plan instantly, picks a provider for each task with costs clear upfront, and follows reminders until move day.

## 4. Goals and success metrics

| Goal | Metric | Target for the pilot |
|---|---|---|
| People find the plan useful | % of sign-ups who build a plan | ≥ 60% |
| The plan drives action | % of plans with at least one booked service | ≥ 30% |
| The move gets fully arranged | % of plans where every task is booked or marked "I'll handle it" | ≥ 25% |
| **North star** | **Moves fully arranged within the customer's budget** | Track weekly |
| Supply is healthy | Live providers per service per metro | ≥ 2 |
| Quality | Average rating on completed bookings | ≥ 4.3 |
| Provider retention | Providers with a booking in the last 30 days | ≥ 50% |

The admin **Customers** page and its CSV export provide the sign-up, plan and booking data for these metrics.

## 5. Scope

### In scope (built)
- Customer accounts, move setup, home addresses with suburb support, and service requirements
- Personalized plan: timeline, tasks, due dates and cost tracking
- Nine bookable services with provider-set tiered pricing
- Provider comparison, profiles, ratings and reviews
- Slot-based instant booking with simulated payment authorization and a 10% platform fee
- Provider self-serve setup, automatic activation, availability calendar, earnings and payouts
- Home photo and video library shared with booked providers
- Booking cancellations (customer or provider), service-issue reporting and resolution
- Admin portal: providers, customers, booking issues, payouts, review moderation, password resets
- Installable mobile app (iPhone home screen, Android APK), a QR code, and a custom domain

### Out of scope (for now)
- Real payment processing (cards, refunds, bank payouts)
- Email and text notifications (blocked until a custom email sender is set up)
- Native App Store and Google Play listings
- Markets outside the Dallas, Houston and Austin metros
- Property manager, broker or employer integrations
- A budget or stipend field and budget guardrails (see section 12)

## 6. User stories

### Customer
1. As a customer, I can sign up with my email and password so my plan is saved.
2. As a customer, I can enter both home addresses, including suburbs like Plano or Katy, so providers know where to go.
3. As a customer, I can describe my home size, access and service needs so prices match my move.
4. As a customer, I get a timeline of tasks with due dates counted back from my move date.
5. As a customer, I can compare providers for each service with a price calculated for my move, inclusions, ratings and availability.
6. As a customer, I can open a provider's profile to see all their services, prices, schedule and reviews.
7. As a customer, I can choose an available date and time slot and have the booking confirmed instantly.
8. As a customer, I can see where my payment goes: the provider's share and Move Me's fee.
9. As a customer, I can upload home photos and a video and share them with my booked providers.
10. As a customer, I can cancel a booking and choose a replacement if a provider cancels.
11. As a customer, I can rate a completed service and report a problem with it.
12. As a customer, I can see my past moves and change my password.

### Provider
1. As a provider, I can create an account and finish my business setup at my own pace, with my progress saved.
2. As a provider, I can choose which services I offer, set my prices for each tier and extra, and pick what's included.
3. As a provider, I can set my working days and time slots, block specific dates, and pause new bookings.
4. As a provider, my listing goes live automatically when setup is complete and my email is confirmed.
5. As a provider, I can see each job's details, addresses, requirements and home media.
6. As a provider, I can mark a job complete, or cancel it with a reason the customer can see.
7. As a provider, I can see expected earnings, pending payouts, payout history and Move Me's fee for every booking.
8. As a provider, I can see my rating and reviews.

### Admin
1. As an admin, I can view every provider and pause or restore a listing with a reason.
2. As an admin, I can see every customer, whether they built a plan, and what they booked, and export the list.
3. As an admin, I can review and resolve service issues. Any held payout is released when the issue is resolved.
4. As an admin, I can see fees earned and payouts, and run a payout check.
5. As an admin, I can hide or restore a review.
6. As an admin, I can reset a customer's or provider's password and give them a temporary one.

## 7. Functional requirements

### 7.1 Accounts and access
- **FR-1** There are three roles: customer, provider and admin. Admin access is granted only in the database.
- **FR-2** Sign-in uses email and password, with a "keep me signed in" option.
- **FR-3** Forgot password sends a reset email (once email is configured). Admins can issue temporary passwords, and signed-in users can change their password.
- **FR-4** Each person sees only their own data. Providers see the customer details for their bookings only.

### 7.2 Move setup and plan
- **FR-5** Address search covers Texas and accepts any address in the Dallas, Houston or Austin metro, matched by county, with manual entry as a fallback.
- **FR-6** The move captures the date, home size, stairs or elevator access, and requirements per service (box range, cleaning level, setup package, handyman hours, storage unit, junk load).
- **FR-7** The plan lists tasks with due dates relative to the move date. Customers can add their own tasks and check them off.
- **FR-8** Completed moves are archived under **Past moves**.

### 7.3 Catalog, pricing and booking
- **FR-9** Each service has fixed tiers (see the README). Providers set a price for every tier, with optional extras: between-city moves and stairs for movers, deep clean for cleaning.
- **FR-10** The price for a move = the provider's tier price for that move + any applicable extras. It is calculated on the server and saved with the booking.
- **FR-11** Only active, unpaused providers serving the customer's metro appear in comparisons.
- **FR-12** Slots are morning or afternoon, one job per slot per provider, within working days, excluding blocked dates, past times and slots already booked. Bookings can be up to 12 months ahead.
- **FR-13** Booking is instant (status *Confirmed*). The fee is 10% of the customer total; the provider receives 90%.
- **FR-14** Payment states are authorized → paid when complete, or released when cancelled. Payout states are not eligible → pending (due the first Friday after completion) → paid, or on hold while an issue is open, or void.

### 7.4 Provider operations
- **FR-15** Setup has three sections that save separately and are protected against conflicting edits in two windows.
- **FR-16** A listing activates automatically when all three sections are complete and the email is confirmed.
- **FR-17** The calendar shows each day's slots and their status. Providers can block or unblock dates and pause new bookings.
- **FR-18** The earnings page shows expected earnings, pending and paid payouts, a ledger per booking, and payout history.

### 7.5 Trust and quality
- **FR-19** Customers can rate (1–5 stars, with an optional comment) only bookings that are completed.
- **FR-20** Ratings show real reviews when there are any; starter listings may show reviews clearly labelled as samples.
- **FR-21** Customers can report an issue on a completed booking. This places a pending payout on hold until an admin resolves it.

### 7.6 Admin
- **FR-22** The Providers page lists every provider with its status, services, prices, availability and earnings, plus pause and restore.
- **FR-23** The Customers page shows summary stats, search, filters, customer details, bookings and a CSV export.
- **FR-24** There are pages for booking issues, payouts and review moderation, and a password reset for customers and providers.

## 8. Non-functional requirements
- **Security:** row-level security on every table; database functions check who is signed in; storage is private, with access to home media limited to the customer and their booked providers.
- **Performance:** a single page loaded once from a CDN, so moving between screens doesn't reload the page.
- **Accessibility:** labelled form fields, keyboard navigation, readable contrast, and screen-reader status messages.
- **Mobile:** works at phone width, installable on iPhone and Android, and the app shell loads offline.
- **Reliability:** the free Supabase plan pauses after about 7 days without activity. Production use requires the Pro plan or regular activity.

## 9. Business model
- **Booking commission:** 10% of every completed booking, included in the customer's price. Customers pay no separate platform fee.
- **Future revenue:** featured provider placement, premium planning tools, and an employer offering (Move Me as the relocation benefit for companies too small for corporate relocation firms).

## 10. Release history

| Date | Release |
|---|---|
| Oct 5–11, 2026 | First MVP: plan, timeline, provider shortlist, customer and provider accounts |
| Oct 11–13 | Providers auto-approved, service checklist, trust details, ratings, photo uploads, item counts |
| Oct 15 | **v3 (Codex build) connected to Supabase:** multi-service providers, instant slot booking, simulated payments and payouts, reviews, booking issues, availability calendar, home media library, admin portal |
| Oct 24 | Custom domain move-me.co with HTTPS |
| Oct 27 | Demo providers removed; installable iPhone app |
| Oct 28 | Suburb addresses supported; Android APK and landing-page download; QR code |
| Oct 30 | Admin Customers page |
| Nov 6 | Admin password reset, Change password, clearer forgot-password messages |

## 11. Roadmap

**Now: validate demand**
- Recruit at least 2 real providers per service in one metro, starting with movers, cleaning and packing.
- Pilot with about 10 people relocating for work, and track the section 4 metrics.
- Connect a custom email sender (Brevo or Resend) for password resets and email confirmation.

**Next: make booking dependable**
- Email notifications: booking confirmed, new job, cancelled, completed.
- A relocation budget or stipend field with "within budget" guidance and a reimbursement summary export.
- Short descriptions for each tier (for example, "Quarter load: about a sofa and a few boxes") so customers choose sizes correctly.
- Supabase Pro plan, so the project never pauses.

**Later: grow**
- Real payments with Stripe Connect.
- Google Play listing, and an App Store listing if adoption justifies it.
- An employer channel for companies that pay relocation stipends.
- New metros, and other life transitions: a first home, starting college.

## 12. Risks and open questions

| Risk or question | Impact | Mitigation |
|---|---|---|
| Very little live supply (1 provider today) | Customers can't book most services | Recruit providers in one metro before promoting to customers |
| No outgoing email | No password resets or confirmations for customers | Custom SMTP; admin reset in the meantime |
| Simulated payments | Not a real transaction yet | Keep it clearly labelled; add Stripe after the pilot shows demand |
| Customers misjudge tier sizes (box count, junk load) | Price disputes on job day | Tier descriptions, home photos and video |
| The landing message is broad ("people who move often") | Weaker pull for the primary segment | Rewrite for professionals relocating with a stipend |
| The budget field from the original concept isn't in the build | The core "modest budget" promise is unproven | Add a stipend field and budget guardrails (Next) |
| Free-plan pausing | The app is down during demos | Weekly activity or the Pro plan |
| Do providers in Fort Worth or Tarrant County serve "Dallas"? | Bookings providers won't take | Confirm with providers, and narrow coverage if needed |
