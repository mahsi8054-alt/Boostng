# BoostNG Founder Journal

> A record of the product decisions, lessons, ideas, and milestones behind BoostNG.

---

## Project

**Name:** BoostNG

**Status:** Pre-development / Architecture

**Initial Market:** Nigeria

**Long-Term Vision:** Expand into additional African and international markets after validating the Nigerian market.

---

# 1. Why BoostNG Exists

BoostNG is being designed as a modern SaaS platform for customers who want to purchase social media growth services through a simple, reliable, and user-friendly platform.

The initial platform will integrate with GoMine as the service provider through its API.

The goal is not simply to create another SMM panel.

The goal is to create a better customer experience around:

- Service discovery
- Ordering
- Wallet management
- Payments
- Order tracking
- Customer support
- Referrals
- Analytics

---

# 2. Initial Market

BoostNG will initially focus on Nigeria.

Primary currency:

NGN

The platform should be architected so that additional countries and currencies can be added later without rebuilding the entire system.

Potential future markets:

- Ghana
- Kenya
- South Africa
- Other African markets
- International markets

---

# 3. Product Philosophy

BoostNG should prioritize:

1. Reliability
2. Security
3. Simplicity
4. Speed
5. Transparency
6. Good customer experience
7. Scalability

The platform should feel like a modern SaaS/fintech product rather than an outdated SMM panel.

---

# 4. Technology Decisions

## Authentication

Clerk

Reason:

Clerk provides a dedicated authentication system and allows authentication logic to remain separate from application data.

---

## Database

Supabase PostgreSQL

Reason:

Supabase provides PostgreSQL, authentication-adjacent infrastructure, storage, database tooling, and a developer-friendly platform.

The project will NOT use Prisma unless a future architectural decision explicitly requires it.

---

## Hosting

Vercel

Reason:

Vercel provides a simple deployment workflow for the Next.js application and integrates naturally with GitHub.

---

## Payments

Initial payment providers:

- Paystack
- Flutterwave

Reason:

These providers are relevant to the initial Nigerian market.

---

## Service Provider

GoMine API

GoMine will act as the external service provider.

BoostNG should keep GoMine integration isolated behind a service layer so another provider can potentially be added in the future.

---

# 5. Architecture Principle

Never tightly couple the entire application to GoMine.

The architecture should look like:

BoostNG

↓

Provider Abstraction

↓

GoMine

Future:

BoostNG

↓

Provider Abstraction

↓

GoMine / Provider B / Provider C

This makes the platform easier to scale and change.

---

# 6. Wallet Philosophy

The wallet is a critical part of BoostNG.

Every balance change must have a corresponding transaction record.

Never silently modify a customer's balance.

Examples:

Deposit

Order Payment

Refund

Referral Bonus

Manual Adjustment

Every operation must be auditable.

---

# 7. Payment Philosophy

Never trust the frontend to confirm a payment.

Payment flow:

Customer

↓

Payment Provider

↓

Provider Webhook

↓

Backend Verification

↓

Wallet Credit

↓

Transaction Record

↓

Notification

Only verified payments should credit a wallet.

---

# 8. Order Philosophy

Customers should be able to place an order with minimal friction.

Order flow:

Service

↓

Quantity

↓

Link

↓

Price

↓

Wallet Check

↓

Payment

↓

GoMine

↓

Status Tracking

The customer should always be able to understand what is happening to their order.

---

# 9. Security Philosophy

Security must be considered from the beginning.

Important principles:

- Never expose secret API keys.
- Never trust client-side balances.
- Never trust frontend payment confirmations.
- Validate every input.
- Protect admin routes.
- Use Row Level Security.
- Log important financial operations.
- Prevent duplicate orders.
- Prevent negative balances.
- Rate-limit sensitive endpoints.

---

# 10. Customer Experience

BoostNG should not feel like a complicated technical system.

Customers should be able to:

- Register quickly.
- Deposit money easily.
- Find services quickly.
- Place orders easily.
- Track orders.
- Understand wallet transactions.
- Contact support.
- Receive notifications.

The interface should be mobile-first because many initial customers will access BoostNG from smartphones.

---

# 11. Design Direction

Design inspiration:

- Stripe
- Vercel
- Linear
- Supabase
- Clerk

Desired characteristics:

- Modern
- Minimal
- Professional
- Fast
- Clean
- Responsive

Themes:

- Light
- Dark
- System

---

# 12. MVP Philosophy

Do not build every future feature before launching.

The first objective is to create a reliable MVP.

Core MVP:

- Landing page
- Authentication
- Services
- Orders
- Wallet
- Deposits
- GoMine integration
- Customer dashboard
- Admin dashboard
- Basic support
- Notifications

Advanced features can follow after validation.

---

# 13. Future Ideas

Potential future features:

- Reseller API
- White-label platform
- Mobile application
- Multi-country support
- Multi-currency
- AI-powered service recommendations
- Advanced analytics
- Team accounts
- Subscription plans
- Bulk ordering
- Affiliate system
- Additional service providers

These ideas should not unnecessarily complicate the MVP.

---

# 14. Important Product Decision

BoostNG should be designed as a platform rather than a single-provider website.

GoMine is the initial provider.

The long-term platform should have the ability to integrate additional providers.

---

# 15. Current Constraints

The project is being planned while development resources are limited.

The founder is currently working primarily from a mobile device and plans to acquire another computer when financially possible.

Therefore:

- Documentation comes first.
- Architecture comes first.
- Development should be phased.
- Avoid unnecessary paid services.
- Prefer free tiers during MVP development.
- Avoid unnecessary infrastructure costs.

The goal is to build intelligently without spending money before the product is ready.

---

# 16. Development Philosophy

Never ask an AI coding agent to blindly generate the entire application at once.

Build in milestones.

Recommended sequence:

1. Foundation
2. Database
3. Authentication
4. UI
5. Wallet
6. Payments
7. GoMine
8. Orders
9. Admin
10. Testing
11. Deployment

Each milestone should be tested before moving forward.

---

# 17. AI Development Philosophy

AI coding tools are assistants, not the final authority.

AI-generated code must be:

- Reviewed
- Tested
- Security checked
- Compared against the specification

The official source of truth is:

`BOOSTNG_MASTER_SPEC.md`

---

# 18. Founder Principle

The goal is not to build the largest platform immediately.

The goal is to build something useful, reliable, and sustainable.

Start small.

Validate.

Improve.

Scale.

---

# 19. Milestone Log

## Milestone 0 — Planning

Status: Completed

- [x] Product concept
- [x] Six-part master specification
- [x] Initial architecture
- [x] Technology decisions
- [x] Development roadmap
- [x] Founder journal

---

## Milestone 1 — Development Environment

Status: Pending

- [ ] Computer available
- [ ] Node.js installed
- [ ] Git installed
- [ ] VS Code installed
- [ ] Repository cloned
- [ ] Development environment configured

---

## Milestone 2 — Foundation

Status: Pending

- [ ] Next.js project
- [ ] Tailwind
- [ ] shadcn/ui
- [ ] Theme system
- [ ] Base layout

---

## Milestone 3 — Authentication

Status: Pending

- [ ] Clerk
- [ ] Sign up
- [ ] Sign in
- [ ] User synchronization
- [ ] Protected routes

---

## Milestone 4 — Database

Status: Pending

- [ ] Supabase schema
- [ ] RLS
- [ ] Database functions
- [ ] Seed data

---

## Milestone 5 — Wallet

Status: Pending

- [ ] Wallet balance
- [ ] Transactions
- [ ] Deposits
- [ ] Refunds
- [ ] Balance protection

---

## Milestone 6 — Payments

Status: Pending

- [ ] Paystack
- [ ] Flutterwave
- [ ] Webhooks
- [ ] Verification

---

## Milestone 7 — GoMine

Status: Pending

- [ ] API client
- [ ] Service synchronization
- [ ] Order creation
- [ ] Status synchronization
- [ ] Error handling

---

## Milestone 8 — Customer Platform

Status: Pending

- [ ] Dashboard
- [ ] Orders
- [ ] Wallet
- [ ] Referrals
- [ ] Coupons
- [ ] Support
- [ ] Notifications

---

## Milestone 9 — Admin Platform

Status: Pending

- [ ] Admin dashboard
- [ ] User management
- [ ] Services
- [ ] Orders
- [ ] Payments
- [ ] Analytics
- [ ] API logs
- [ ] Audit logs

---

## Milestone 10 — Launch

Status: Pending

- [ ] Security review
- [ ] Testing
- [ ] Production deployment
- [ ] Domain
- [ ] Monitoring
- [ ] Backup strategy
- [ ] Launch

---

# 20. Decision Log

Use this section to record important future decisions.

Format:

### Decision: [Title]

**Date:**

**Decision:**

**Reason:**

**Alternatives considered:**

**Impact:**

---

# 21. Lessons Learned

Use this section throughout development.

### Lesson 1

_To be documented._

### Lesson 2

_To be documented._

### Lesson 3

_To be documented._

---

# 22. Future Founder Notes

This section is intentionally left open.

Ideas, observations, customer feedback, business opportunities, and lessons can be recorded here.

---

# Final Principle

Build something people want.

Keep it simple.

Protect the customer's money.

Protect the customer's data.

Make the experience better.

Then scale.
