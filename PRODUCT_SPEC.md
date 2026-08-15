
# Business Storefront MVP — Product Specification
**Product:** Business Storefront  
**Document:** Product Specification  
**Version:** 1.0  
**Status:** Approved MVP Baseline  
**Primary Operator:** Product owner / Admin  
**Target Market:** Small Nigerian businesses selling through WhatsApp and social media

---

# 1. Product Definition

## 1.1 One-sentence definition

Business Storefront is a simple, professional digital storefront that gives a small business one shareable link where customers can view what the business sells, prices, location, delivery information, opening hours, and contact options, then start an order through WhatsApp.

## 1.2 Product positioning

Business Storefront is:

> A digital storefront + WhatsApp ordering bridge.

It is **not** a full e-commerce platform.

The MVP does not process payments, manage deliveries, manage inventory, or automatically process WhatsApp conversations.

---

# 2. Product Problem

Many small businesses already sell through:

- WhatsApp
- Instagram
- Facebook
- TikTok
- Physical shops
- Word of mouth

However, customers often need to ask basic questions before buying:

- What do you sell?
- How much does it cost?
- Where are you located?
- Do you deliver?
- What areas do you deliver to?
- When are you open?
- How do I order?

Business Storefront gives the business one professional link containing the essential information.

Example:

`yourapp.com/ada-bakes`

A customer should be able to open that link and understand the business without first having to start a conversation.

---

# 3. MVP Objective

The MVP must allow the admin to:

1. Create a business.
2. Add the business information.
3. Add products or services.
4. Publish the storefront.
5. Give the business a unique public URL.
6. Generate a QR code for the storefront.
7. Allow customers to browse the storefront.
8. Allow customers to start a WhatsApp order.
9. Track basic storefront interactions through admin-only analytics.

---

# 4. MVP Success Criterion

The MVP is considered successful when the following complete journey works reliably:

```text
Admin
  ↓
Create Business
  ↓
Add Business Information
  ↓
Add Products
  ↓
Preview
  ↓
Publish
  ↓
Receive Unique URL + QR Code

Customer
  ↓
Open URL
  ↓
Understand Business
  ↓
Browse Products
  ↓
Select Product
  ↓
Click WhatsApp
  ↓
WhatsApp Opens
  ↓
Pre-filled Message Appears
  ↓
Customer Sends Message
If this journey works reliably on a real mobile device, the core MVP objective has been achieved.
5. Users and Roles
The MVP has three interaction groups.
5.1 Admin
The product owner is the only authenticated operator during the MVP.
The admin can:
Create businesses
View businesses
Edit businesses
Preview businesses
Publish businesses
Unpublish businesses
Delete businesses
Add products
Edit products
Delete products
Change product prices
Change product availability
Mark products as popular
Upload and replace images
View basic analytics
Copy storefront URLs
Access QR codes
Generate/provide digital business cards
There are no additional staff roles in the MVP.
5.2 Business Owner
Business owners do not have accounts in the MVP.
They do not log into the application.
The admin collects their information manually and creates/manages their storefront.
The business owner receives the resulting assets, such as:
Public storefront URL
QR code
Digital business card
A business-owner dashboard may be considered in a future version, but it is explicitly outside the MVP.
5.3 Customer
Customers are public visitors.
Customers do not need an account.
Customers can:
Open a public storefront
View business information
Browse products/services
View prices
See product availability
View delivery information
View opening hours
Click WhatsApp
Click social links
Customers cannot:
Access the admin area
Edit business information
Modify products
View private analytics
Create customer accounts
Access another business's administrative information
6. Core Customer Journey
The primary customer journey is:
Receive Business Link
        ↓
Open Storefront
        ↓
Understand Business
        ↓
Browse Products
        ↓
Find Desired Product
        ↓
Click "Order on WhatsApp"
        ↓
WhatsApp Opens
        ↓
Pre-filled Message Appears
        ↓
Customer Reviews/Edits Message
        ↓
Customer Sends Message
This journey should require minimal friction.
The application must not force customers to:
Register
Log in
Complete an online checkout
Enter payment information
Create an account
7. Public Storefront
The public storefront is the primary customer-facing product experience.
It must be mobile-first, clear, fast, and professional.
7.1 Public URL
Every business receives a unique public URL.
Examples:
yourapp.com/ada-bakes
yourapp.com/tolu-fashion
yourapp.com/freshcut-barbers
The URL uses a readable slug.
Example:
Business name: Ada Bakes
Slug: ada-bakes
7.2 Slug requirements
A business slug must be:
Unique
URL-safe
Human-readable
Stable
Case-insensitive in practice
A slug collision must never cause one business to overwrite or display another business.
If a desired slug already exists, the system must use an alternative unique slug or require the admin to resolve the conflict.
The system must never rely on a database ID as the primary public URL.
8. Storefront Header
The storefront should prominently display:
Business logo/profile image
Business name
Business category
Short business description
Cover/hero image
Location
Example:
ADA BAKES
Fresh homemade bread & pastries in Lekki, Lagos
9. Primary Call to Action
The primary customer action is:
Order on WhatsApp
This CTA must be visually prominent.
It should be easy to find without navigating through complicated menus.
The customer should immediately understand how to contact/order from the business.
10. Products and Services
A business can have multiple products or services.
Each product/service may contain:
Product/service image
Name
Description
Price
Availability status
Popular indicator
Example:
Agege Bread
Freshly baked every morning.
₦2,500
Available
[Order on WhatsApp]
Products belong to exactly one business.
A product must never accidentally appear on another business's storefront.
11. Product Price
The MVP is designed primarily for Nigerian businesses.
Prices should support Nigerian Naira.
Example:
₦2,500
The interface should display prices clearly and consistently.
The MVP does not process payments.
12. Product Availability
Each product must have an availability state.
Minimum states:
Available
Unavailable
The admin must be able to change availability without deleting and recreating the product.
When a product is unavailable:
The storefront must clearly indicate that it is unavailable.
The customer should not be presented with an active order action for that unavailable product.
The exact visual treatment is a UI decision, but the state must be obvious.
13. Popular Products
The admin may mark a product as:
Popular
This is a presentation feature only.
The Popular state:
Does not change price.
Does not change availability.
Does not affect ordering.
Does not create a separate product type.
It simply allows the storefront to highlight products the business considers important or popular.
14. WhatsApp Ordering
WhatsApp ordering is a core MVP capability.
14.1 Business-level WhatsApp CTA
The storefront must provide a prominent WhatsApp action.
Example:
Order on WhatsApp
The action opens WhatsApp using the business's configured WhatsApp number.
The message may contain a simple business-level greeting.
14.2 Product-level WhatsApp CTA
Available products should provide a product-specific WhatsApp action.
Example:
Order on WhatsApp
The generated message should identify the business and product.
Example:
Hi Ada Bakes, I'd like to order Agege Bread.
The customer must be able to review or edit the message before sending it.
15. WhatsApp Scope Limitation
The MVP does not use the WhatsApp Business API.
The product does not:
Automatically send WhatsApp messages
Automatically receive WhatsApp messages
Automatically process orders
Automatically reply to customers
Run WhatsApp bots
The expected flow is:
Customer clicks WhatsApp
        ↓
WhatsApp opens
        ↓
Message is pre-filled
        ↓
Customer reviews/edits
        ↓
Customer sends message
The actual conversation and order handling remain on WhatsApp.
16. Business Information
A storefront can display:
Location
Delivery areas
Opening hours
WhatsApp
Phone number
Instagram
Facebook
TikTok
Only information provided by the business should be displayed.
The system must never invent missing business information.
17. Delivery Information
Businesses may specify delivery areas.
Example:
Lekki
Ikoyi
Victoria Island
If delivery information is not provided, the storefront should not fabricate or imply delivery coverage.
The MVP does not calculate delivery fees or provide delivery tracking.
18. Opening Hours
Businesses may provide opening hours.
Example:
Monday–Saturday
8:00 AM–7:00 PM
The storefront should present opening hours clearly.
The MVP does not need automated booking or appointment scheduling.
19. Social Links
The MVP supports:
Required/core:
WhatsApp
Optional:
Instagram
Facebook
TikTok
Phone
A social/contact button must only appear when valid information has been provided.
Empty social buttons must not be displayed.
20. Mobile-first Requirement
Mobile experience is a non-negotiable MVP requirement.
The storefront is expected to receive significant traffic from:
WhatsApp
Instagram
Facebook
TikTok
QR codes
Many visitors will use mobile devices.
The storefront must therefore prioritize:
Readable text
Large touch targets
Clear prices
Good product images
Simple navigation
Prominent WhatsApp CTA
Comfortable scrolling
Minimal clutter
The application must also work properly on desktop and larger screens.
However:
Mobile experience takes priority.
21. Performance Requirements
The public storefront should feel fast on ordinary mobile connections.
The MVP should avoid unnecessary:
Animations
Heavy dependencies
Huge images
External services
JavaScript
Complex visual effects
Images should be appropriately optimized.
Performance should be treated as part of product quality, not as an optional enhancement.
22. Admin Area
The admin area is private.
A minimum conceptual structure is:
/admin
    Dashboard
    Businesses
    Analytics
The exact visual navigation may change during implementation provided the required capabilities remain intact.
23. Admin Authentication
The MVP requires protected admin authentication.
Only the authorized admin should be able to access management functionality.
The MVP does not require:
Customer authentication
Business-owner authentication
Staff authentication
Multiple admin roles
Authentication implementation details belong in the technical architecture documentation.
24. Business Management
The admin must be able to:
Create
Create a new business.
View
View business information.
Edit
Modify business information.
Preview
View the storefront before making it public.
Publish
Make the storefront publicly accessible.
Unpublish
Temporarily remove the storefront from public access without losing its data.
Delete
Permanently remove a business when necessary.
Destructive deletion must require an explicit confirmation.
The implementation should avoid accidental deletion.
25. Business Publication States
A business has a publication state.
Minimum states:
Draft
Published
Unpublished
Draft
The storefront is being prepared.
It is not publicly available as a normal storefront.
Published
The storefront is publicly accessible.
Unpublished
The storefront is no longer publicly accessible, but the business and its data remain available to the admin.
Unpublishing must not delete the business.
26. Admin Product Management
The admin must be able to:
Add products
Edit products
Delete products
Change prices
Change availability
Upload/change product images
Mark/unmark products as Popular
Products must remain associated with the correct business.
27. Image Management
The MVP supports images for:
Business
Logo/profile image
Cover/hero image
Products
Product/service image
Images must be stored separately from the main business/product records.
The database should store the appropriate reference to each image.
Image storage and access rules belong to the technical architecture.
28. QR Code
Each business must have a QR code pointing to its public storefront.
Example:
Scan to view Ada Bakes
[ QR CODE ]

yourapp.com/ada-bakes
The QR code must point to the storefront URL, not directly to WhatsApp.
Reason:
The storefront remains the business's central destination.
This also allows the storefront experience to evolve without requiring a new QR destination.
The QR code should be available to the admin as a usable/downloadable asset.
29. Digital Business Card
The MVP should provide a simple digital business card asset.
Example:
ADA BAKES

Fresh bread & pastries

📍 Lekki, Lagos

Scan to view menu & order

[ QR CODE ]
The objective is to provide a useful business asset.
The product is not intended to recreate Canva or become a graphic-design platform.
The exact visual design may evolve as long as the resulting asset is clean and useful.
30. Analytics
Analytics are admin-only in the MVP.
Businesses and customers cannot access the analytics dashboard.
The MVP tracks basic interactions.
Minimum events:
Storefront page view
WhatsApp click
Instagram click
Facebook click
TikTok click
Where practical, product-specific WhatsApp clicks should identify the associated product.
31. Analytics Philosophy
The MVP is not a full analytics platform.
We do not need:
Complex charts
Funnels
Heatmaps
Visitor profiles
Advanced attribution
Customer tracking
Marketing automation
The purpose is simply to help the admin understand whether storefronts are being viewed and interacted with.
Example:
ADA BAKES

Page views        127
WhatsApp clicks    34
Instagram clicks   12
32. Analytics Event Model
Analytics should conceptually use a general event model.
An event contains:
Business
Event type
Optional product
Timestamp
Possible event types:
page_view
whatsapp_click
instagram_click
facebook_click
tiktok_click
This approach leaves room for future event types without requiring a separate analytics system for every metric.
33. Analytics Privacy
Analytics are internal product metrics.
The MVP must not expose private analytics to public visitors.
The system should collect only the information necessary for the defined MVP metrics.
The MVP does not require building a customer identity database.
34. Basic SEO and Social Sharing
Each public storefront should have appropriate basic metadata.
At minimum:
Page title
Description
Business name
Relevant preview image
The objective is to make shared storefront links appear professional on platforms that support link previews.
The MVP does not include an advanced SEO management system.
35. Public Page Errors
The application must gracefully handle:
Invalid business URL
Non-existent business
Unpublished business
Missing product image
Business with no products
Failed data loading
Invalid information
Network failures
The customer should receive a useful message or page rather than a blank or broken screen.
36. Loading States
Appropriate loading feedback should exist where information may take time to load.
Important areas include:
Public storefront
Admin business list
Business editing
Product management
Image uploads
Analytics
Loading states should be simple and purposeful.
37. Empty States
The application must handle legitimate empty conditions.
Examples:
Business has no products
Show an appropriate message instead of displaying a broken product section.
No businesses
The admin should see a useful empty state.
No analytics yet
Show a useful zero-state rather than a broken chart.
Empty data is not an application error.
38. Error Feedback
Errors should be:
Understandable
Visible
Actionable where possible
Appropriate to the context
The system should avoid exposing raw technical errors to customers.
For example, a customer should not see database error messages or internal implementation details.
39. Security Requirements
Security is a core MVP requirement.
Public access
Public visitors may access only information intentionally published for storefront display.
Admin access
Administrative functionality must be protected.
Database
Administrative and private information must not be publicly exposed through unrestricted database access.
Secrets
Private credentials and secrets must never be committed to GitHub.
Environment variables
Sensitive configuration must be handled through environment configuration.
Validation
Administrative input must be validated before being stored or used.
Authorization
Authentication alone is not sufficient.
The system must also ensure that authenticated users have the appropriate permissions to perform administrative actions.
40. Public vs Private Information
Public information
The following may appear on a published storefront:
Business name
Category
Description
Logo
Cover image
Products
Product descriptions
Prices
Product availability
Popular status
Location
Delivery areas
Opening hours
WhatsApp
Phone
Social links
Private information
The following must remain protected:
Admin credentials
Authentication information
Private analytics
Internal administrative data
Database/security information
Private configuration
Secrets
Internal system information
The public must never gain administrative access by discovering a URL.
41. Content Integrity
The system must not invent business information.
Examples:
If the business does not provide delivery areas:
Do not create delivery areas.
If the business does not provide Instagram:
Do not display an Instagram link.
If the business has no products:
Display an appropriate empty state.
The product should represent the business accurately rather than generate unsupported claims.
42. Business Validation
Before publishing, the admin must provide enough information to create a credible storefront.
The minimum business information should include:
Business name
Category
Description
WhatsApp number
Location
Unique slug
Product information should include:
Product/service name
Price
Availability state
Image requirements should be determined by the final implementation based on whether a credible storefront can be produced without them.
The system must clearly communicate missing information that prevents publishing.
43. Data Model — Product Requirements
The MVP requires records representing at least:
Businesses
Products
Analytics Events
Business
A business needs to represent:
Unique identifier
Name
Unique slug
Category
Description
Logo
Cover image
Location
Delivery information
Opening hours
WhatsApp
Phone
Social links
Publication state
Creation timestamp
Update timestamp
Product
A product needs to represent:
Unique identifier
Owning business
Name
Description
Price
Image
Availability
Popular state
Creation timestamp
Update timestamp
Analytics Event
An analytics event needs to represent:
Unique identifier
Business
Event type
Optional product
Timestamp
Exact database types, indexes, constraints, relationships, and security policies belong in DATABASE.md.
44. URL Requirements
Public business URLs must be:
Readable
Unique
Stable
Mobile-friendly
Directly resolvable
Independent of exposed database IDs
Preferred:
/ada-bakes
Not:
/business/8291837
45. Admin Workflow
The intended admin workflow is:
ADMIN LOGIN
     ↓
CREATE BUSINESS
     ↓
ENTER BUSINESS INFORMATION
     ↓
UPLOAD LOGO/COVER
     ↓
ADD PRODUCTS
     ↓
UPLOAD PRODUCT IMAGES
     ↓
SET PRICES
     ↓
SET AVAILABILITY
     ↓
PREVIEW
     ↓
PUBLISH
     ↓
COPY URL
     ↓
ACCESS QR CODE
     ↓
PROVIDE BUSINESS ASSETS
46. Customer Workflow
The intended customer workflow is:
CUSTOMER RECEIVES LINK
        ↓
OPENS STOREFRONT
        ↓
SEES BUSINESS
        ↓
BROWSES PRODUCTS
        ↓
SELECTS PRODUCT
        ↓
CLICKS WHATSAPP
        ↓
WHATSAPP OPENS
        ↓
PRE-FILLED MESSAGE
        ↓
CUSTOMER SENDS MESSAGE
47. Testing Standard
A feature is not considered complete merely because its interface exists.
Every major feature must be tested for:
Normal behavior
The intended action works.
Empty behavior
The feature behaves correctly when no data exists.
Invalid behavior
Invalid or incomplete information is handled appropriately.
Failure behavior
Network, database, upload, or other expected failures produce useful feedback.
Mobile behavior
The feature works on an actual mobile device.
Security behavior
Users cannot access information or functionality they are not authorized to access.
48. Minimum End-to-End Acceptance Test
The MVP must successfully pass this complete test:
Admin logs in.
Admin creates a business.
Admin enters valid business information.
Admin uploads business images.
Admin creates at least two products.
Admin sets product prices.
Admin changes product availability.
Admin marks a product as Popular.
Admin previews the storefront.
Admin publishes the business.
Public storefront URL works.
Business information displays correctly.
Products display correctly.
Prices display correctly.
Availability is displayed correctly.
WhatsApp CTA works.
Product WhatsApp CTA generates the correct product message.
Customer can edit the message before sending.
Social links work when configured.
QR code resolves to the storefront.
Digital business card contains correct business information.
Page view analytics are recorded.
WhatsApp click analytics are recorded.
Social click analytics are recorded.
Admin can view the analytics.
Admin can edit the business.
Admin can edit products.
Admin can unpublish the business.
Unpublished storefront is no longer publicly accessible.
Admin can republish the business.
Admin can delete a business with confirmation.
Invalid URLs receive a useful not-found experience.
Empty states work correctly.
Loading states work correctly.
The complete experience works on a real mobile device.
49. Performance and Quality Baseline
The MVP should prioritize:
Fast initial storefront loading
Optimized images
Responsive layout
Minimal unnecessary dependencies
Clear loading states
Clear error states
Reliable navigation
Reliable WhatsApp links
Reliable public URLs
Secure admin access
The product does not need enterprise-level infrastructure at MVP stage.
However, poor engineering practices that create obvious security, reliability, or maintainability problems are not acceptable merely because this is an MVP.
50. Design Principles
The public storefront should feel:
Professional
It should look like a legitimate business storefront, not a generic unfinished template.
Simple
Customers should understand the page quickly.
Mobile-first
The primary experience is designed around smartphones.
Trustworthy
Business information should be clear and consistent.
Fast
Avoid unnecessary visual and technical weight.
Action-oriented
The customer should naturally reach the WhatsApp ordering action.
Consistent
Different businesses may have different content and imagery, while the overall product experience remains coherent.
51. Admin Design Principles
The admin interface should prioritize:
Speed
Clarity
Simple editing
Minimal unnecessary clicks
Obvious actions
Useful feedback
Safe destructive actions
The admin may eventually manage many businesses, so repetitive tasks should remain practical.
52. MVP Technology Direction
The approved technology direction is:
Area
Technology
Application
Next.js
Database
Supabase
Authentication
Supabase Auth
Image Storage
Supabase Storage
Source Control
GitHub
Primary AI Development Environment
Kiro
Secondary AI Development Environment
Windsurf
UI / Design Assistance
v0
Cloud Development Environment
GitHub Codespaces
Production Hosting
Render
Rapid Prototyping / Independent Projects
Hostinger Horizons
Architecture and Product Intelligence
ChatGPT
Technology choices may be changed only through deliberate review.
AI coding agents must not silently replace the approved stack because another technology appears convenient.
53. Tool Responsibilities
Each tool has a defined role.
ChatGPT
Responsible for:
Product reasoning
Planning
Architecture review
Requirements clarification
Technical reasoning
Troubleshooting
Code review assistance
Testing strategy
Security review
Quality control
Scope control
ChatGPT is not the project's source of truth.
The repository is.
v0
Primarily responsible for:
UI exploration
Visual design
Storefront interface concepts
Component/interface ideas
Responsive design exploration
v0 should not become an independent production backend.
Kiro
Primary application development environment.
Responsible for implementing approved requirements and technical plans.
Kiro must follow the project's repository documentation and must not independently expand the MVP.
Windsurf
Secondary development environment.
Used when:
Kiro reaches a usage limitation
A second development environment is useful
A problem requires another AI coding perspective
The project owner chooses Windsurf for a particular implementation task
The existing GitHub repository remains the source of truth.
GitHub
Permanent source of truth for the project.
It stores:
Application source code
Project documentation
Project history
Configuration that is safe to commit
Version history
No AI development tool owns the project.
GitHub Codespaces
Provides a cloud development environment connected to the GitHub repository.
It is a development workspace, not the production host and not the application's database.
Supabase
Responsible for the application's backend data services, including:
Database
Authentication
Image/file storage
Required backend services
Exact implementation is defined in the technical architecture.
Render
Responsible for production hosting/deployment of the main application.
The expected production relationship is:
GitHub
   ↓
Render
   ↓
Live Application
   ↓
Supabase
Hostinger Horizons
Horizons is not part of the required core production pipeline for this MVP.
Its approved role is:
Rapid prototypes
Independent experiments
Small standalone websites
Quick client projects
Demonstrations
Testing ideas before committing them to the main product
A prototype created in Horizons must not automatically be treated as production architecture for the main Business Storefront application.
If an idea proves valuable, it can later be deliberately redesigned and implemented within the main GitHub/Supabase/Render architecture.
54. Source of Truth
The project's source of truth is:
The GitHub repository.
The following are development tools, not project ownership systems:
ChatGPT
Kiro
Windsurf
v0
Codespaces
Horizons
The application must remain portable between development tools.
For example:
Kiro → Windsurf
must not require rebuilding the application from the beginning.
55. Project Documentation
The repository should contain, at minimum:
README.md
PRODUCT_SPEC.md
PROJECT_RULES.md
ARCHITECTURE.md
DATABASE.md
Kiro-specific project instructions and steering documentation may exist under:
.kiro/
The documentation must remain synchronized with major architectural decisions.
56. Development Rules
The project must be developed incrementally.
The preferred cycle is:
PLAN
  ↓
SPECIFY
  ↓
IMPLEMENT
  ↓
INSPECT
  ↓
TEST
  ↓
FIX
  ↓
REVIEW
  ↓
COMMIT
  ↓
NEXT TASK
AI agents must not blindly generate the entire application in one uncontrolled operation.
57. Change Control
A change should be evaluated before implementation.
Questions:
Is the change required for the MVP?
Does it solve a real user problem?
Does it conflict with the product specification?
Does it introduce unnecessary complexity?
Does it affect security?
Does it affect the database?
Does it affect existing businesses or URLs?
Can it be safely added later?
If a change is outside the MVP, it should normally be deferred rather than implemented immediately.
58. Explicit MVP Scope Protection
The following features are explicitly outside the MVP:
Client dashboard
Client login
Customer accounts
Staff accounts
Client template selection
Client analytics
Subscription system
Payment gateway
Online payment
E-commerce checkout
Inventory management
POS
CRM
Delivery tracking
WhatsApp Business API
WhatsApp automation
AI chatbot
Customer database
Email marketing
Advanced analytics
Custom domains
Advanced SEO management
Automated business onboarding
Multi-admin permissions
Staff roles
Complex order management
Automated order processing
These may be considered in future versions.
They must not be added to the MVP merely because they are technically possible.
59. MVP Non-goals
The product does not attempt to replace:
WhatsApp
Instagram
Facebook
TikTok
Shopify
POS systems
Inventory systems
CRMs
Payment processors
Delivery companies
The product's purpose is narrower:
Give a business a professional digital front door and connect customers to the business through WhatsApp.
60. Future Expansion Principle
The MVP should be built cleanly enough that future functionality can be added without unnecessarily rebuilding the entire system.
Potential future capabilities may include:
Business-owner accounts
Client dashboards
Client analytics
Online payments
Order management
Booking
Inventory
Customer management
WhatsApp automation
AI assistance
Subscriptions
Custom domains
Advanced analytics
None of these are commitments.
Future features must be based on real user/business feedback rather than assumptions.
61. MVP Completion Rule
When the MVP acceptance criteria are satisfied:
STOP BUILDING NEW FEATURES.
The next priority becomes real-world validation.
The product should be tested with approximately 3–5 real Nigerian businesses.
The admin should observe:
What businesses understand immediately
What businesses find confusing
What customers interact with
Where customers hesitate
Whether WhatsApp ordering is actually used
Whether businesses value the storefront
What businesses request next
Real-world evidence should determine the next product iteration.
62. Final Product Principle
The MVP follows this principle:
Build the smallest thing that genuinely works, verify it aggressively, protect it carefully, and only then make it bigger.
The objective is not to build the largest possible platform.
The objective is to build a small product that solves one problem extremely well:
Give a Nigerian business one professional link that helps customers understand what they sell and start an order through WhatsApp.
63. Final Definition of Done
The Business Storefront MVP is DONE when:
The admin can take a real small Nigerian business, enter its information, add its products, publish its storefront, provide its unique link and QR code, and a normal customer can open that link on a phone, understand the business, browse its products, and start an order through WhatsApp.
At that point:
STOP.
Do not add unrelated features.
Move to:
REAL BUSINESSES
      ↓
REAL CUSTOMERS
      ↓
REAL FEEDBACK
      ↓
MEASURE
      ↓
LEARN
      ↓
DECIDE
      ↓
VERSION 2
64. Product Authority
This document is the approved product baseline for Business Storefront MVP v1.
If an implementation decision conflicts with this document, the conflict must be identified and resolved deliberately.
AI coding agents must not silently reinterpret the product requirements.
Changes to the product scope should be intentional, documented, and reviewed before implementation.
End of Product Specification v1
