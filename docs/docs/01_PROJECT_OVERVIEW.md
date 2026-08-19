BoostNG — Project Overview

Document: 01_PROJECT_OVERVIEW.md
Version: 1.0
Status: Pre-Development
Initial Market: Nigeria
Primary Currency: NGN

---

1. Project Overview

BoostNG is a modern SaaS platform that allows customers to purchase social media growth services through a simple, secure, and mobile-first interface.

The platform will initially operate in Nigeria and use GoMine as the primary service provider through its API.

Customers will be able to:

- Create an account.
- Browse available social media services.
- Deposit money into their BoostNG wallet.
- Place orders.
- Track order progress.
- Receive notifications.
- Earn referral rewards.
- Use promotional coupons.
- Contact customer support.

Administrators will have a separate management platform for controlling users, services, orders, payments, pricing, referrals, support, analytics, and GoMine synchronization.

---

2. Product Vision

The long-term vision of BoostNG is to become a reliable social-growth marketplace that provides a significantly better experience than traditional SMM panels.

The product should prioritize:

1. Reliability
2. Security
3. Simplicity
4. Speed
5. Transparency
6. Customer experience
7. Scalability

BoostNG should feel like a modern SaaS or fintech product rather than an outdated social-media panel.

---

3. Initial Target Market

The MVP will initially target customers in Nigeria.

Initial configuration

Country: Nigeria

Currency: Nigerian Naira (NGN)

Language: English

Payment Providers:

- Paystack
- Flutterwave

The architecture must remain flexible enough to support additional countries and currencies later.

Potential future markets include:

- Ghana
- Kenya
- South Africa
- Other African markets
- International markets

---

4. Target Customers

BoostNG is intended to serve:

Creators

People who use social media to build an audience, personal brand, or business.

Businesses

Businesses that need social-media visibility and marketing services.

Digital Marketers

Marketing professionals managing social accounts and campaigns.

Resellers

Future customers who may use BoostNG's API to offer services through their own platforms.

Agencies

Future customers managing multiple clients and social-media campaigns.

---

5. Core Customer Journey

The primary customer journey is:

Landing Page
      ↓
Create Account
      ↓
Clerk Authentication
      ↓
Customer Dashboard
      ↓
Browse Services
      ↓
Select Service
      ↓
Enter Link
      ↓
Enter Quantity
      ↓
Calculate Price
      ↓
Wallet Balance Check
      ↓
Create Order
      ↓
GoMine API
      ↓
Track Order
      ↓
Completed

The process should be simple enough for a new customer to understand without technical knowledge.

---

6. Core MVP Features

The first production version should include:

Authentication

- Clerk sign up
- Clerk sign in
- Protected routes
- User profile
- Role-based authorization

Services

- Service categories
- Service list
- Service descriptions
- Minimum quantity
- Maximum quantity
- Customer pricing
- Service status

Wallet

- Wallet balance
- Deposits
- Transactions
- Order deductions
- Refunds
- Referral rewards

Payments

- Paystack
- Flutterwave
- Payment verification
- Webhooks
- Deposit history

Orders

- Create order
- Order validation
- GoMine submission
- Order status
- Order history
- Order details
- Automatic status synchronization

Customer Dashboard

- Overview
- Orders
- Wallet
- Transactions
- Referrals
- Coupons
- Notifications
- Support
- Profile
- Settings

Admin Dashboard

- Overview
- User management
- Service management
- Order management
- Wallet management
- Deposits
- Withdrawals
- Coupons
- Referrals
- Support
- Analytics
- GoMine controls
- API logs
- Audit logs
- System settings

---

7. Technology Stack

Frontend

Next.js

Use a modern Next.js architecture with TypeScript.

Styling

Tailwind CSS

UI

shadcn/ui

Icons

Lucide

Animation

Framer Motion

Authentication

Clerk

Database

Supabase PostgreSQL

Storage

Supabase Storage

Hosting

Vercel

Payments

Paystack

Flutterwave

Service Provider

GoMine API

---

8. Authentication Architecture

Clerk is responsible for authentication.

Supabase is responsible for application data.

Conceptually:

Customer
   ↓
Clerk
   ↓
Authenticated Session
   ↓
BoostNG Application
   ↓
Supabase

Authentication secrets must never be exposed to the client.

Administrative authorization must be enforced on the backend as well as through frontend route protection.

---

9. Database Architecture

Supabase PostgreSQL will store application data.

The database will contain records for areas including:

- Users
- Profiles
- Wallets
- Transactions
- Services
- Categories
- Orders
- Payments
- Referrals
- Coupons
- Notifications
- Support Tickets
- API Logs
- Audit Logs

The exact schema is defined separately in:

docs/03_DATABASE.md

---

10. GoMine Integration

GoMine will initially be the primary external service provider.

BoostNG will communicate with GoMine through a dedicated backend service layer.

Conceptually:

BoostNG
   ↓
GoMine Service Layer
   ↓
GoMine API

The GoMine API key must remain server-side.

The frontend must never receive or expose the GoMine API key.

The integration should support, where available:

- Service synchronization
- Balance checking
- Order creation
- Order status checking
- Order synchronization
- Error handling
- Retry handling

Detailed GoMine architecture will be documented in:

docs/05_GOMINE_API.md

---

11. Payment Architecture

Customers will be able to fund their BoostNG wallet through supported Nigerian payment providers.

Initial providers:

- Paystack
- Flutterwave

Payment flow:

Customer
   ↓
Select Deposit Amount
   ↓
Payment Gateway
   ↓
Payment Provider
   ↓
Webhook
   ↓
Backend Verification
   ↓
Wallet Credit
   ↓
Transaction Record
   ↓
Notification

The frontend must never be trusted as proof that a payment succeeded.

Only verified backend payment events can credit a wallet.

---

12. Wallet Architecture

The wallet is a core financial component.

Every balance change must produce a corresponding transaction record.

Examples:

Deposit
Order Payment
Refund
Referral Reward
Manual Adjustment

The system must:

- Prevent negative balances.
- Prevent duplicate transactions.
- Use transactional database operations where necessary.
- Maintain an immutable transaction history where practical.
- Record the reason for administrative adjustments.

Detailed wallet architecture will be documented in:

docs/07_WALLET_SYSTEM.md

---

13. Order Architecture

Orders are created after validating:

- Customer authentication
- Service availability
- Quantity
- URL
- Wallet balance
- Coupon
- Service limits

Order flow:

Customer
   ↓
Select Service
   ↓
Enter Order Information
   ↓
Calculate Price
   ↓
Validate
   ↓
Check Wallet
   ↓
Create Local Order
   ↓
Deduct Wallet
   ↓
Submit to GoMine
   ↓
Save GoMine Order ID
   ↓
Track Status

Order status may include:

- Pending
- Processing
- Completed
- Partial
- Cancelled
- Failed

The local BoostNG order remains the source of truth for the customer's order history.

---

14. Pricing Architecture

GoMine's service cost and BoostNG's customer price must be separated.

Example:

GoMine Cost:       ₦100
BoostNG Markup:     30%
Customer Price:    ₦130
Profit:             ₦30

Administrators should be able to configure:

- Global markup
- Category markup
- Service markup
- Fixed pricing
- Percentage pricing

The pricing engine must calculate the final customer price server-side.

---

15. Referral System

Customers can receive referral rewards when eligible users join through their referral link or code.

The referral system should support:

- Referral codes
- Referral links
- Referral tracking
- Commission calculations
- Referral earnings
- Referral history

Referral rules should be configurable by administrators.

---

16. Coupon System

Administrators can create promotional coupons.

Coupons may support:

- Percentage discounts
- Fixed discounts
- Minimum order amount
- Maximum discount
- Usage limits
- Expiration dates
- User-specific restrictions

Coupon calculations must be validated server-side.

---

17. Notification System

The platform should notify customers about important events.

Examples:

- Order created
- Order processing
- Order completed
- Order failed
- Deposit successful
- Withdrawal update
- Referral reward
- Coupon
- Support response
- System announcement

The MVP should support in-app notifications.

Email notifications can be added later without requiring SMTP during the initial MVP.

---

18. Support System

Customers should be able to create support tickets.

A ticket can contain:

- Subject
- Category
- Priority
- Message
- Status
- Created date
- Updated date

Administrators can:

- Reply
- Change status
- Change priority
- Add internal notes
- Close tickets
- Reopen tickets

---

19. Admin Platform

The admin platform is responsible for operating BoostNG.

Administrators should be able to manage:

- Users
- Services
- Categories
- Orders
- Wallets
- Payments
- Coupons
- Referrals
- Support
- Notifications
- Analytics
- GoMine
- API logs
- Audit logs
- System settings

Admin functionality must be protected by server-side role authorization.

---

20. User Interface

BoostNG will use a mobile-first responsive design.

Supported:

- Mobile
- Tablet
- Desktop
- Large displays

Themes:

- Light
- Dark
- System

The interface should use:

- Clean typography
- Consistent spacing
- Accessible components
- Clear status indicators
- Loading states
- Empty states
- Error states
- Success feedback

The UI should not resemble a generic template or outdated SMM panel.

---

21. Security Principles

Security is a core product requirement.

The system must:

- Protect environment variables.
- Never expose secret API keys.
- Validate all server inputs.
- Protect admin routes.
- Use Supabase Row Level Security.
- Prevent negative wallet balances.
- Prevent duplicate order submissions.
- Verify payment webhooks.
- Rate-limit sensitive endpoints.
- Log important financial operations.
- Avoid exposing internal errors.
- Sanitize user-controlled content.

A complete security specification will be maintained in:

docs/10_SECURITY.md

---

22. Scalability

The initial MVP should remain simple while avoiding architectural decisions that make future growth difficult.

The architecture should be capable of evolving from:

100 users
   ↓
1,000 users
   ↓
10,000 users
   ↓
100,000 users
   ↓
1,000,000+ users

Scaling infrastructure should only be introduced when actual usage requires it.

Avoid unnecessary paid infrastructure during MVP development.

---

23. Development Strategy

Development will happen in controlled phases.

Phase 1

Project foundation and design system.

Phase 2

Clerk authentication.

Phase 3

Supabase database.

Phase 4

Customer dashboard.

Phase 5

Wallet.

Phase 6

Payments.

Phase 7

GoMine integration.

Phase 8

Order engine.

Phase 9

Admin dashboard.

Phase 10

Testing, security review, and deployment.

Every phase should leave the application in a working state.

---

24. Documentation Strategy

The following documents will contain detailed technical specifications:

docs/
├── 01_PROJECT_OVERVIEW.md
├── 02_SYSTEM_ARCHITECTURE.md
├── 03_DATABASE.md
├── 04_AUTHENTICATION.md
├── 05_GOMINE_API.md
├── 06_PAYMENT_SYSTEM.md
├── 07_WALLET_SYSTEM.md
├── 08_ORDER_ENGINE.md
├── 09_ADMIN_SYSTEM.md
├── 10_SECURITY.md
├── 11_DEPLOYMENT.md
├── 12_UI_GUIDELINES.md
├── 13_BRAND_GUIDE.md
└── 14_FUTURE_ROADMAP.md

The master specification remains the overall product source of truth.

Technical documents provide deeper implementation details.

---

25. Definition of Success

BoostNG MVP is considered ready for launch when:

- Authentication works reliably.
- Users can deposit funds.
- Wallet balances are accurate.
- Services are synchronized correctly.
- Customers can create orders.
- Orders are successfully submitted to GoMine.
- Order statuses synchronize correctly.
- Admins can manage the platform.
- Payment verification is secure.
- Financial transactions are auditable.
- Mobile UX is polished.
- Security checks have been completed.
- Production deployment is stable.

---

26. Current Status

Project Stage: Planning / Architecture

Completed:

- [x] Product concept
- [x] Initial market definition
- [x] Technology stack
- [x] Master specification
- [x] Roadmap
- [x] Task tracking
- [x] Founder journal
- [x] Project overview

Next:

- [ ] System architecture
- [ ] Database architecture
- [ ] Authentication architecture
- [ ] GoMine API specification
- [ ] Payment architecture
- [ ] Wallet architecture
- [ ] Order engine architecture
- [ ] Admin architecture
- [ ] Security architecture
- [ ] Deployment architecture
- [ ] UI guidelines
- [ ] Brand guide

---

27. Source of Truth

When conflicts occur between implementation decisions and documented requirements, review:

1. "BOOSTNG_MASTER_SPEC.md"
2. Relevant document inside "docs/"
3. "FOUNDER_JOURNAL.md"
4. "ROADMAP.md"

Important architectural decisions should be documented before making major changes.

---

Document Ownership

Project: BoostNG

Document: Project Overview

Version: 1.0

Status: Active

Last Updated: 2026-08-19
