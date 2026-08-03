BoostNG v1.0 – Master Prompt (Part 1)
1. Project Overview
You are a Senior Full-Stack Software Architect and Senior UI/UX Designer.
Build a production-ready SaaS application named BoostNG.
BoostNG is a Social Media Growth Platform that allows creators, influencers, marketers, agencies, and businesses to purchase social media growth services through a clean wallet-based system.
The backend automatically connects to the GoMine API for order creation and order synchronization.
The platform launches in Nigeria but is designed to expand internationally.
This is not an SMM panel clone.
Instead, it should feel like a premium SaaS similar to:
Stripe
Clerk
Linear
Vercel
Notion
Framer
The application must be modern, beautiful, responsive, scalable, secure, and production-ready.
2. Core Objectives
The platform should allow customers to:
Create an account
Verify their email using Clerk
Deposit funds into their wallet
Purchase social media services
Track order progress
Receive in-app notifications
Contact support
View wallet history
Use coupons
Earn referral commissions
Administrators should be able to:
Manage users
Manage orders
Manage pricing
Manage services
Manage deposits
Approve withdrawals
View revenue
View analytics
Configure the entire platform
3. Target Market
Phase 1
🇳🇬 Nigeria
Phase 2
Ghana
Kenya
South Africa
Phase 3
Worldwide
The system should be multi-currency ready even if only NGN is enabled initially.
4. Technology Stack
Frontend
Next.js 15 App Router
React
TypeScript
Tailwind CSS
shadcn/ui
Framer Motion
React Hook Form
Zod
next-themes
Authentication
Use Clerk.
Do NOT build custom authentication.
Support
Email
Password
Google Login
Password Reset
Email Verification
Session Management
User Profile
Protected Routes
Clerk Middleware
Clerk Webhooks
Never store passwords.
Database
Use Supabase.
Do NOT use Prisma.
Use
PostgreSQL
Row Level Security
Supabase Storage
Supabase JavaScript SDK
Payments
Integrate
Paystack
Flutterwave
Architecture must allow adding
Stripe
USDT
TON
Crypto
later.
External API
Integrate
GoMine API
Functions
List Services
Create Order
Check Status
Check Balance
5. Product Branding
Name
BoostNG
Logo
Modern minimalist logo using:
Gold
Black
White
Typography
Use Geist or Inter.
Rounded corners.
Professional fintech feel.
6. Design System
The application should look like a premium fintech SaaS.
Do NOT use generic Bootstrap styling.
Use:
Large spacing
Rounded cards
Glassmorphism (subtle)
Soft shadows
Gradient highlights
Beautiful loading animations
Premium icons (Lucide)
Micro-interactions
Responsive layouts
Accessible color contrast
7. Theme System
Implement a complete theme engine.
Support:
🌞 Light
🌙 Dark
💻 System
Use next-themes.
Remember user preference.
Theme toggle in navbar.
Every page must support all themes.
Dark Theme
Background
#090909
Cards
#151515
Sidebar
#101010
Accent
Gold (#F5B301)
Text
White
Secondary Text
Gray
Light Theme
Background
White
Cards
#F7F7F8
Sidebar
White
Accent
Gold
Text
Dark Gray
8. Navigation
Top Navigation
Logo
Search
Notifications
Theme Toggle
Wallet Balance
Profile Menu
Sidebar
Dashboard
Wallet
New Order
Orders
Transactions
Referrals
Coupons
Support
Settings
9. Landing Page
Sections
Hero
Trusted By
Features
How It Works
Statistics
Why Choose BoostNG
Pricing
Testimonials
FAQ
Footer
Hero Section
Large modern hero.
Headline
Grow Your Social Media With Confidence
Subheadline
Purchase premium engagement services with instant order processing, secure payments, and real-time tracking.
Buttons
Start Growing
Explore Services
10. Homepage Statistics
Display live counters.
Examples
Orders Completed
Customers
Available Services
Countries Supported
Success Rate
11. Features Section
Cards
Instant Delivery
Secure Wallet
Fast Deposits
GoMine Powered
Live Tracking
Referral Rewards
Premium Support
Affordable Pricing
12. Dashboard Overview
After login, users land on a modern dashboard.
Cards
Wallet Balance
Pending Orders
Completed Orders
Today's Spending
Referral Earnings
Coupons Available
Notifications
Recent Activity
Recent Transactions
13. Responsive Design
Support
Desktop
Tablet
Mobile
Large Screens
Use mobile-first design.
14. Accessibility
Keyboard navigation.
ARIA labels.
High contrast.
Accessible forms.
Readable typography.
15. Performance
Lazy loading.
Image optimization.
Code splitting.
Server Components.
Fast page transitions.
SEO optimization.
16. Important Development Rules
The AI must:
Build all pages completely.
Do not use placeholder pages.
Do not stop development because API keys are missing.
Use mock data until real credentials are provided.
Do not request SMTP credentials.
Use in-app notifications only.
Build reusable components.
Follow clean architecture.
Use TypeScript everywhere.
Use environment variables for external services.
Write production-quality code.
Create a complete README with setup instructions.










BoostNG v1.0 – Master Prompt (Part 2)
Database Architecture (Supabase + Clerk)
Database
Use Supabase PostgreSQL.
Do NOT use Prisma.
Do NOT use Firebase.
Use:
Supabase PostgreSQL
Supabase Storage
Supabase JavaScript SDK
SQL Migrations
Row Level Security (RLS)
Authentication
Use Clerk.
Never store passwords.
Synchronize Clerk users into Supabase using Clerk Webhooks.
Supported webhook events:
user.created
user.updated
user.deleted
The application must automatically create, update, and delete users in Supabase.
Database Tables
users
Columns
id UUID PRIMARY KEY

clerk_id TEXT UNIQUE

email TEXT

full_name TEXT

username TEXT UNIQUE

avatar_url TEXT

phone TEXT

country TEXT DEFAULT 'Nigeria'

currency TEXT DEFAULT 'NGN'

wallet_balance NUMERIC DEFAULT 0

total_spent NUMERIC DEFAULT 0

total_deposited NUMERIC DEFAULT 0

referral_code TEXT UNIQUE

referred_by UUID

role TEXT DEFAULT 'user'

status TEXT DEFAULT 'active'

created_at TIMESTAMP

updated_at TIMESTAMP
services
id UUID PRIMARY KEY

gomine_service_id INTEGER

category TEXT

name TEXT

description TEXT

minimum INTEGER

maximum INTEGER

cost_price NUMERIC

selling_price NUMERIC

profit NUMERIC

status BOOLEAN

created_at TIMESTAMP

updated_at TIMESTAMP
orders
id UUID PRIMARY KEY

user_id UUID

service_id UUID

gomine_order_id TEXT

link TEXT

quantity INTEGER

cost_price NUMERIC

selling_price NUMERIC

profit NUMERIC

status TEXT

start_count INTEGER

remaining INTEGER

created_at TIMESTAMP

updated_at TIMESTAMP
Status values
Pending
Processing
Completed
Partial
Cancelled
Failed
wallet_transactions
id UUID PRIMARY KEY

user_id UUID

reference TEXT

type TEXT

amount NUMERIC

balance_before NUMERIC

balance_after NUMERIC

status TEXT

description TEXT

created_at TIMESTAMP
Types
Deposit
Withdrawal
Order
Refund
Bonus
Referral
Adjustment
deposits
id UUID PRIMARY KEY

user_id UUID

amount NUMERIC

payment_method TEXT

gateway_reference TEXT

status TEXT

proof TEXT

created_at TIMESTAMP
Status
Pending
Approved
Rejected
withdrawals
id UUID PRIMARY KEY

user_id UUID

amount NUMERIC

bank_name TEXT

account_number TEXT

account_name TEXT

status TEXT

created_at TIMESTAMP
coupons
id UUID PRIMARY KEY

code TEXT UNIQUE

discount_type TEXT

discount_value NUMERIC

minimum_purchase NUMERIC

maximum_discount NUMERIC

usage_limit INTEGER

used_count INTEGER

expires_at TIMESTAMP

status BOOLEAN
coupon_usage
id UUID PRIMARY KEY

coupon_id UUID

user_id UUID

order_id UUID

created_at TIMESTAMP
referrals
id UUID PRIMARY KEY

referrer_id UUID

referred_user_id UUID

commission NUMERIC

status TEXT

created_at TIMESTAMP
notifications
id UUID PRIMARY KEY

user_id UUID

title TEXT

message TEXT

type TEXT

read BOOLEAN

created_at TIMESTAMP
Types
Order
Deposit
Withdrawal
Referral
Coupon
System
Support
support_tickets
id UUID PRIMARY KEY

user_id UUID

subject TEXT

priority TEXT

status TEXT

created_at TIMESTAMP

updated_at TIMESTAMP
Priority
Low
Medium
High
Urgent
ticket_messages
id UUID PRIMARY KEY

ticket_id UUID

sender_type TEXT

message TEXT

attachment TEXT

created_at TIMESTAMP
api_logs
id UUID PRIMARY KEY

provider TEXT

endpoint TEXT

request JSONB

response JSONB

status INTEGER

created_at TIMESTAMP
settings
id UUID PRIMARY KEY

key TEXT

value TEXT

updated_at TIMESTAMP
Wallet Architecture
Every user owns a wallet.
Wallet balance is stored in
users.wallet_balance
Every transaction creates a record in
wallet_transactions
Never update wallet balance without creating a transaction.
Wallet Logic
Deposit
↓
Wallet Balance +
↓
Transaction Record
↓
Notification
↓
Dashboard Update
Order
↓
Wallet Balance -
↓
Create Order
↓
Transaction Record
↓
Submit to GoMine
↓
Notification
Refund
↓
Wallet Balance +
↓
Transaction Record
↓
Notification
Referral Bonus
↓
Wallet Balance +
↓
Transaction Record
↓
Notification
Referral System
Every user automatically receives a referral code.
Example
BOOSTA9K21
When a new user registers using the referral code
↓
Save referred_by
↓
After first successful deposit
↓
Credit commission
↓
Notify referrer
Admin configures referral percentage.
Coupon Engine
Coupons support
Percentage Discount
Fixed Amount
Free Service (future)
Expiry
Usage Limits
One-time Use
Per User Limit
Coupon validation happens before payment.
Notification System
No SMTP.
No email required.
Use in-app notifications.
Notification Bell
Unread Count
Read/Unread
Delete
Filter by Type
Notifications for
Deposit
Withdrawal
Order Completed
Order Failed
Referral Bonus
Support Reply
System Maintenance
Support Center
Users can
Open Ticket
Reply
Close Ticket
Attach Screenshots
Admins can
Reply
Assign Priority
Close Ticket
Reopen Ticket
Search System
Global search should search
Orders
Services
Transactions
Support Tickets
Users (Admin)
Filters
Orders
By Status
By Date
By Service
By Category
Transactions
By Type
By Date
Support
By Status
By Priority
Clerk Middleware
Protect
/dashboard
/orders
/wallet
/settings
/support
/admin
Unauthenticated users
↓
Redirect to
/sign-in
Admin Roles
Store role in database
role = user
role = admin
Admin routes require
Admin Role
Clerk Authentication
Row Level Security (RLS)
Enable RLS on all user-owned tables.
Users can only access:
Their own orders
Their own wallet
Their own notifications
Their own deposits
Their own withdrawals
Their own support tickets
Their own referral data
Admins have elevated access through secure backend logic.
Never expose unrestricted database access from the client.
Folder Structure
/app
  /(marketing)
  /(auth)
  /(dashboard)
  /(admin)

/components
  /ui
  /dashboard
  /wallet
  /orders
  /notifications
  /support

/lib
  supabase/
  clerk/
  auth/

 /services
  gomine/
  payments/
  wallet/

 /hooks

 /types

 /utils

 /public

 middleware.ts
Development Rules
Use Server Components where appropriate.
Use Server Actions for secure mutations.
Validate all forms with Zod.
Keep business logic separate from UI.
Create reusable hooks and services.
Never hardcode API keys.
Use environment variables for all secrets.
Use optimistic UI updates where appropriate.
Ensure all database writes are transactional where possible.





BoostNG v1.0 – Master Prompt (Part 3)
GoMine API Architecture & Order Processing Engine
GoMine Integration
Create a dedicated service layer named:
/services/gomine
Never call the GoMine API directly from UI components.
All requests must go through the backend.
Environment Variables
GOMINE_API_URL=https://app.gomine.social/api/v2

GOMINE_API_KEY=

GOMINE_TIMEOUT=30000

GOMINE_MAX_RETRIES=3
GoMine Service
Create a reusable API client.
Functions:
getBalance()

getServices()

createOrder()

checkOrderStatus()

cancelOrder() // if GoMine supports it

syncServices()

syncOrders()
Every function must:
Validate inputs
Catch errors
Log responses
Retry temporary failures
Return typed responses
API Request Structure
Use
POST
Content-Type
application/x-www-form-urlencoded
Never expose the API key on the frontend.
Only the backend communicates with GoMine.
Service Synchronization
Admin Dashboard
↓
Sync Services
↓
Fetch latest services from GoMine
↓
Update local database
↓
Add new services
↓
Update existing prices
↓
Disable unavailable services
Never duplicate services.
Local Services
BoostNG should NOT rely on GoMine for displaying services.
Instead:
GoMine
↓
Sync
↓
Supabase
↓
Website displays local database
Advantages
Faster loading
Better SEO
Custom pricing
Better filtering
Independent of GoMine uptime
Pricing Engine
Every service contains
Cost Price
Selling Price
Profit
Markup %
Admin controls
Fixed Markup
Percentage Markup
Example
GoMine Cost

₦100

↓

Markup

30%

↓

Selling Price

₦130

↓

Profit

₦30
Prices should automatically update when admin changes markup.
Order Flow
Customer
↓
Select Category
↓
Select Service
↓
Enter Link
↓
Enter Quantity
↓
Apply Coupon (optional)
↓
Calculate Price
↓
Wallet Balance Check
↓
Deduct Wallet
↓
Create Local Order
↓
Submit To GoMine
↓
Receive GoMine Order ID
↓
Save GoMine Order ID
↓
Show Success Screen
Order Validation
Before creating order
Validate
Minimum Quantity
Maximum Quantity
Valid URL
Wallet Balance
Service Enabled
Coupon
User Status
Reject invalid orders.
Order Status
Support
Pending
Processing
Completed
Partial
Cancelled
Failed
Update automatically.
Background Worker
Create
/services/workers
Workers
Order Sync Worker
Service Sync Worker
Notification Worker
Referral Worker
Daily Analytics Worker
Order Sync Worker
Runs every minute.
Workflow
Pending Orders

↓

Check Status

↓

Update Database

↓

Notify User

↓

Refresh Dashboard
Completed Orders
When order becomes
Completed
↓
Update Order
↓
Create Notification
↓
Dashboard Refresh
↓
Analytics Update
Partial Orders
If GoMine returns Partial
↓
Save Remaining
↓
Save Delivered Count
↓
Notify Customer
Failed Orders
If GoMine returns Failed
↓
Refund Wallet (optional, configurable)
↓
Create Wallet Transaction
↓
Notify Customer
↓
Log Error
Retry System
Temporary errors
↓
Retry
1
↓
Retry
2
↓
Retry
3
↓
Fail
↓
Log Error
↓
Notify Admin
API Logs
Every API request creates
api_logs
Store
Provider
Endpoint
Request
Response
HTTP Status
Execution Time
Timestamp
Admins can search logs.
Queue System
Avoid sending hundreds of requests simultaneously.
Implement queue.
Order Queue
↓
GoMine API
↓
Response
↓
Database
Future-ready for Redis or message queues.
Dashboard Statistics
User Dashboard
Wallet
Orders
Transactions
Pending
Completed
Spent Today
Referral Earnings
Admin Dashboard
Revenue Today
Revenue Month
Orders Today
Orders Month
GoMine Balance
Top Services
Active Users
New Registrations
Profit
Conversion Rate
Payment Flow
Deposit
↓
Gateway
↓
Webhook
↓
Verify
↓
Credit Wallet
↓
Transaction
↓
Notification
↓
Dashboard
Never trust frontend payment responses.
Always verify via backend.
Withdrawal Flow
User
↓
Withdrawal Request
↓
Pending
↓
Admin Review
↓
Approve
↓
Wallet Deduction
↓
Transaction
↓
Notification
Refund System
Admin can refund
Entire Order
Partial Order
Manual Amount
Refund
↓
Wallet
↓
Transaction
↓
Notification
Wallet Protection
Never allow negative balance.
All balance updates must use transactions.
Never update wallet directly.
Duplicate Order Protection
Prevent
Double Click
Browser Refresh
Multiple Requests
Use idempotency tokens.
Rate Limiting
Limit
Order Creation
Deposits
Withdrawals
Login
Support Tickets
API endpoints
Security
Validate
Quantity
URLs
Coupon
Balance
User
Role
Sanitize every input.
Reseller API (Future Ready)
Create architecture for public API.
Endpoints
POST /api/v1/order

GET /api/v1/status

GET /api/v1/services

GET /api/v1/balance
API Keys
Rate Limits
Usage Logs
Future feature—not enabled in MVP.
Notifications
Generate notifications for:
Order Created
Order Processing
Order Completed
Order Failed
Deposit Approved
Withdrawal Approved
Coupon Applied
Referral Bonus
Support Reply
System Maintenance
Analytics Engine
Calculate:
Daily Revenue
Monthly Revenue
Total Revenue
Profit
Average Order Value
Customer Lifetime Value
Repeat Customers
Best Selling Services
Conversion Rate
Search & Filters
Orders:
Status
Category
Service
Date
User
Transactions:
Type
Date
Amount
Users:
Email
Username
Role
Status
Error Handling
Create global error handler.
User-friendly messages.
Log technical details.
Never expose internal errors.
Folder Structure
/services
    /gomine
        client.ts
        orders.ts
        services.ts
        sync.ts
        balance.ts

    /payments
        paystack.ts
        flutterwave.ts

    /wallet

    /analytics

    /notifications

    /workers
Code Standards
Use TypeScript interfaces for all API responses.
Separate controllers, services, and utilities.
No business logic in React components.
Use async/await consistently.
Log external API failures.
Implement retry and timeout handling.
Write code with future scaling in mind.

BoostNG v1.0 – Master Prompt (Part 4)
Customer Dashboard & User Experience
Customer Experience Goal
The customer dashboard should feel like a modern fintech application, not a traditional SMM panel.
Design inspiration:
Stripe
Linear
Vercel
Clerk
Notion
Requirements:
Fast
Beautiful
Mobile-first
Responsive
Smooth animations
Light/Dark/System themes
Clean typography
Consistent spacing
Accessible UI
Dashboard Home
After login, redirect users to:
/dashboard
Display a personalized greeting:
Good Morning, John 👋
or
Welcome back, John!
Dashboard Cards
Top section:
Wallet Balance
Pending Orders
Completed Orders
Total Spent
Referral Earnings
Active Coupons
Each card should include:
Icon
Value
Trend indicator
Optional percentage change
Smooth hover animation
Quick Actions
Display large action buttons:
New Order
Deposit Funds
Wallet
Order History
Support
Invite Friends
Recent Activity
Show latest:
Deposits
Orders
Refunds
Referral rewards
Coupon usage
Include:
Status badge
Date
Amount
Service name
Quick View button
Notification Center
Bell icon in navbar.
Features:
Unread counter
Mark all as read
Delete notification
Filter notifications
Notification categories:
Orders
Wallet
Referral
Coupons
Support
System
Each notification should open the related page.
Wallet Page
Route:
/dashboard/wallet
Display:
Current Balance
Total Deposited
Total Spent
Referral Earnings
Pending Withdrawals
Wallet Actions
Buttons:
Deposit
Withdraw
Transaction History
Transaction History
Columns:
Date
Reference
Description
Amount
Balance
Status
Type
Support:
Search
Filter
Pagination
CSV Export (future-ready)
Deposit Page
Route:
/ dashboard/wallet/deposit
Payment methods:
Paystack
Flutterwave
Manual Bank Transfer
Workflow:
Choose amount
↓
Select payment method
↓
Complete payment
↓
Backend verifies payment
↓
Wallet credited
↓
Success page
Withdraw Page
Route:
/dashboard/wallet/withdraw
Fields:
Amount
Bank Name
Account Number
Account Name
Validation:
Minimum withdrawal
Maximum withdrawal
Wallet balance check
Confirmation modal before submission.
Order Page
Route:
/dashboard/orders/new
Steps:
Select Category
Select Service
Read service description
Enter link
Enter quantity
Apply coupon
Review order
Submit
Price Calculator
Calculate in real time:
Cost
Discount
Total
Estimated Delivery
Minimum
Maximum
Disable submit if validation fails.
Order Success Page
Display:
Success animation
Order ID
Service
Quantity
Amount
Current Status
Button:
View Order
Orders Page
Route:
/dashboard/orders
Features:
Search
Filter
Pagination
Status badges
Sorting
Columns:
Order ID
Service
Link
Quantity
Amount
Status
Created Date
Actions
Order Details
Clicking an order opens:
Order information
Timeline
Status
GoMine Order ID
Start Count
Remaining
Price
Coupon Used
Transaction Reference
Support Button
Status Timeline
Example:
🟢 Order Created
↓
🟡 Submitted to GoMine
↓
🟡 Processing
↓
🟢 Completed
Favorites
Allow users to:
Favorite services
Recently ordered services
Quick reorder
Referral Dashboard
Route:
/dashboard/referrals
Display:
Referral Code
Referral Link
Total Referrals
Total Earnings
Pending Earnings
Referral History
Buttons:
Copy Link
Share
Invite Friends
Coupon Center
Route:
/dashboard/coupons
Display:
Available Coupons
Used Coupons
Expired Coupons
Apply Coupon
Coupon Details
Support Center
Route:
/dashboard/support
Display:
Open Tickets
Closed Tickets
Create Ticket
Knowledge Base
FAQ
Tick
