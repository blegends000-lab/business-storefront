Absolutely. We should make ARCHITECTURE.md implementation-ready but not over-specify things that belong in DATABASE.md or actual code.

One important correction from the earlier plan: I’m going to keep this architecture document tightly aligned with the approved PRODUCT_SPEC.md v1. It will define system boundaries, components, data flow, security boundaries, deployment, development workflow, and portability between Kiro/Windsurf—without inventing extra MVP functionality.

# Business Storefront MVP — System Architecture

**Product:** Business Storefront  
**Document:** System Architecture  
**Version:** 1.0  
**Status:** Approved MVP Architecture Baseline  
**Related Documents:** `README.md`, `PRODUCT_SPEC.md`, `PROJECT_RULES.md`  
**Primary Production Host:** Render  
**Primary Backend Services:** Supabase  
**Primary Source of Truth:** GitHub  

---

# 1. Purpose

This document defines the technical structure and boundaries of the Business Storefront MVP.

It describes:

- the major parts of the system
- how those parts communicate
- where application code lives
- where application data lives
- how public and private functionality are separated
- how images are handled
- how analytics flow through the system
- how the application is developed and deployed
- how the project remains portable between AI development tools
- the technical boundaries that must be respected during MVP development

This document explains **how the approved product is structured**.

It does not replace `PRODUCT_SPEC.md`.

`PRODUCT_SPEC.md` defines **what the product must do**.

`PROJECT_RULES.md` defines **how the project must be developed and maintained**.

This document defines **how the system is organized to support those requirements**.

---

# 2. Architecture Principles

The architecture must follow these principles:

1. Keep the MVP simple.
2. Prefer the smallest architecture that reliably satisfies the product requirements.
3. Keep public storefront functionality separate from administrative functionality.
4. Keep sensitive administrative operations protected.
5. Keep application source code independent from any particular AI coding tool.
6. Keep the database and storage responsibilities centralized in Supabase.
7. Keep production hosting centralized in Render.
8. Keep GitHub as the permanent source of truth.
9. Avoid introducing unnecessary external services.
10. Avoid building infrastructure for features that are explicitly outside the MVP.
11. Preserve the ability to expand the product later without unnecessarily rebuilding the foundation.
12. Do not allow AI coding agents to silently change the approved architecture.
13. Security and data protection must be considered before implementation, not after deployment.
14. Every architectural change must be deliberate and documented.

---

# 3. High-Level System

The MVP consists of the following major parts:

```text
                         ┌─────────────────────┐
                         │      Customers      │
                         └──────────┬──────────┘
                                    │
                                    │ Public storefront
                                    ▼
                         ┌─────────────────────┐
                         │  Business Storefront│
                         │      Application    │
                         └──────────┬──────────┘
                                    │
                 ┌──────────────────┼──────────────────┐
                 │                  │                  │
                 ▼                  ▼                  ▼
          Business Data       Image Storage       Analytics
                 │                  │                  │
                 └──────────────────┼──────────────────┘
                                    ▼
                              ┌────────────┐
                              │  Supabase  │
                              └────────────┘


                         ┌─────────────────────┐
                         │       Admin         │
                         └──────────┬──────────┘
                                    │
                                    │ Protected access
                                    ▼
                         ┌─────────────────────┐
                         │   Admin Interface   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                              ┌────────────┐
                              │  Supabase  │
                              └────────────┘

The application is the central interface.

Supabase provides the application's backend data services.

Render hosts the production application.

GitHub stores the application source code and project documentation.


---

4. Approved Technology Direction

The approved MVP technology direction is:

Responsibility	Technology

Application	Next.js
Database	Supabase
Authentication	Supabase Auth
Image/File Storage	Supabase Storage
Source Control	GitHub
Primary AI Development Environment	Kiro
Secondary AI Development Environment	Windsurf
UI / Design Assistance	v0
Cloud Development Environment	GitHub Codespaces
Production Hosting	Render
Rapid Prototyping / Independent Projects	Hostinger Horizons
Architecture / Product Intelligence	ChatGPT


These technologies have defined responsibilities.

A tool must not be introduced into another responsibility merely because it is convenient.


---

5. System Boundaries

The MVP consists of the following functional boundaries:

PUBLIC STOREFRONT
        │
        ├── Business information
        ├── Products/services
        ├── Prices
        ├── Availability
        ├── Delivery information
        ├── Opening hours
        ├── Contact/social links
        └── WhatsApp actions


ADMIN AREA
        │
        ├── Authentication
        ├── Business management
        ├── Product management
        ├── Publishing controls
        ├── Image management
        ├── QR access
        ├── Digital business card access
        └── Analytics


BACKEND SERVICES
        │
        ├── Database
        ├── Authentication
        ├── Image storage
        └── Analytics event storage

The architecture does not include backend infrastructure for features explicitly excluded from the MVP.


---

6. Application Structure

The application should logically separate:

Application
│
├── Public Storefront
│
├── Admin Area
│
├── Shared UI / Presentation
│
├── Data Access
│
├── Authentication
│
├── Image Handling
│
├── WhatsApp Link Generation
│
├── QR Code Generation/Access
│
└── Analytics Event Recording

The exact source-code folder structure may be determined during implementation, provided the separation of responsibilities remains clear.

AI coding agents must not create an unnecessarily complicated folder structure simply for the sake of architectural appearance.


---

7. Public Storefront Architecture

The public storefront is the customer-facing portion of the application.

A customer accesses a storefront through a public business slug.

Example:

/ada-bakes

The application uses the slug to identify the requested business.

Conceptually:

Customer
   ↓
Public URL
   ↓
Business Slug
   ↓
Business Lookup
   ↓
Publication Check
   ↓
Public Business Data
   ↓
Storefront

Only businesses that are allowed to be publicly displayed should resolve as normal public storefronts.


---

8. Public Storefront Data Boundary

The public storefront must receive only information intended for public display.

Public storefront information may include:

business name

category

description

logo

cover image

products

product descriptions

prices

availability

popular status

location

delivery areas

opening hours

WhatsApp

phone

social links


The public storefront must not receive:

admin credentials

private authentication information

private analytics

internal administrative information

secrets

private configuration

unnecessary internal system information


The architecture must enforce this boundary rather than relying only on the interface to hide information.


---

9. Published Business Resolution

A public business URL must resolve according to the business publication state.

Conceptually:

Requested Slug
      ↓
Find Business
      ↓
Does Business Exist?
   ┌──┴──┐
  No    Yes
  ↓      ↓
404    Check State
         │
     ┌───┼─────────────┐
     ↓   ↓             ↓
   Draft Published  Unpublished
     ↓     ↓             ↓
   Not   Show          Not
 Public Storefront     Public

A business that is not published must not be displayed as a normal public storefront.

Unpublishing must preserve the business data for the admin.


---

10. URL Architecture

Public business URLs must use readable slugs.

Preferred:

/ada-bakes

Not:

/business/8291837

The slug must be:

unique

URL-safe

human-readable

stable

safe against collisions


The public URL must not depend on exposing an internal database identifier.

If a business name conflicts with an existing slug, the system must ensure that two businesses never resolve to the same public URL.


---

11. Admin Architecture

The admin area is a protected portion of the application.

Conceptually:

Admin
  ↓
Authentication
  ↓
Authorization
  ↓
Admin Interface
  ↓
Protected Operations
  ↓
Supabase

The admin interface provides the controls required by the approved MVP.

These include:

business creation

business editing

business deletion

publishing

unpublishing

preview

product management

image management

analytics access

QR access

digital business card access



---

12. Authentication Boundary

The MVP requires protected admin access.

The authentication system must distinguish an authorized administrator from an unauthenticated public visitor.

Public visitors:

Public Storefront
     ↓
No admin authentication required

Admin:

Admin Login
     ↓
Authenticated Session
     ↓
Authorized Admin Access

Authentication does not automatically grant permission to perform every possible backend operation.

Authorization must also be enforced.

The MVP does not require:

customer accounts

business-owner accounts

staff accounts

multiple admin roles



---

13. Authorization Principle

The application must verify authorization for protected administrative operations.

Examples include:

creating businesses

editing businesses

deleting businesses

changing publication state

managing products

managing images

viewing analytics


A hidden button is not a security control.

A URL being difficult to guess is not a security control.

Authorization must be enforced at the appropriate backend/data-access boundary.


---

14. Supabase Responsibilities

Supabase is responsible for the application's backend data services.

For the MVP, this includes:

Supabase
│
├── Database
├── Authentication
└── Storage

The database stores structured application information.

Supabase Auth handles the approved admin authentication mechanism.

Supabase Storage handles the application's image/file storage requirements.

The exact database structure and security policies are defined separately in DATABASE.md.


---

15. Database Boundary

The database is the persistent source of application data.

At minimum, the system requires records representing:

Businesses
Products
Analytics Events

The database must maintain the relationship:

Business
   │
   └── Products

Each product belongs to exactly one business.

Analytics events must identify the relevant business and may optionally identify a product.

Exact tables, columns, types, indexes, relationships, constraints, and security policies belong in:

DATABASE.md

They should not be invented independently by an AI coding agent during implementation.


---

16. Image Storage Boundary

Images are stored separately from structured business/product records.

The expected relationship is:

Application
    ↓
Supabase Storage
    ↓
Image/File

The database stores the appropriate reference needed to associate an image with the relevant business or product.

Images may include:

business logo

business cover image

product image

digital business card assets where appropriate


The final storage visibility and access policies must be deliberately defined in DATABASE.md and the implementation.


---

17. Image Upload Flow

Conceptually:

Admin
  ↓
Select Image
  ↓
Validate Image
  ↓
Upload
  ↓
Supabase Storage
  ↓
Store Image Reference
  ↓
Business/Product Record

The system should handle expected upload failures gracefully.

The application should not save an invalid or unusable image reference merely because an upload attempt was initiated.

The exact image size, format, naming, and validation rules belong in the implementation and technical documentation after verification.


---

18. Product Architecture

Products/services are subordinate to a business.

Conceptually:

Business
   │
   ├── Product 1
   ├── Product 2
   ├── Product 3
   └── Product N

A product contains the information required by the approved product specification.

The system must prevent accidental cross-business association.

A product belonging to Business A must not appear on Business B's storefront.


---

19. Product Availability

Product availability is part of the product's stored state.

Minimum states:

Available
Unavailable

The public storefront uses this state to determine how the product is presented.

Unavailable products must not be presented as normally orderable products.

The admin must be able to change availability without recreating the product.


---

20. WhatsApp Architecture

The MVP uses WhatsApp deep links.

It does not use the WhatsApp Business API.

Conceptually:

Customer
   ↓
WhatsApp CTA
   ↓
Generated WhatsApp Link
   ↓
WhatsApp
   ↓
Pre-filled Message
   ↓
Customer Sends

The application does not control the WhatsApp conversation after the customer leaves the storefront.

The MVP does not:

send messages automatically

receive messages automatically

process WhatsApp orders automatically

run WhatsApp bots

maintain WhatsApp conversations



---

21. WhatsApp Link Generation

Business-level and product-level WhatsApp actions may generate different messages.

Business-level:

Business WhatsApp Number
        ↓
WhatsApp Link
        ↓
Optional Business Greeting

Product-level:

Business WhatsApp Number
        ↓
Product Context
        ↓
Generated Message
        ↓
WhatsApp Link

Example:

Hi Ada Bakes, I'd like to order Agege Bread.

The customer must remain in control of sending the message.

The application must not claim that an order has been completed merely because a WhatsApp link was clicked.


---

22. Analytics Architecture

Analytics use an event-based approach.

Conceptually:

Customer Interaction
        ↓
Event
        ↓
Analytics Recording
        ↓
Supabase
        ↓
Admin Analytics

Minimum event types include:

page_view
whatsapp_click
instagram_click
facebook_click
tiktok_click

A product-specific WhatsApp event may identify the product when applicable.


---

23. Analytics Data Boundary

Analytics are admin-only.

Public visitors must not be able to access private analytics data.

The analytics system should collect only the information required for the approved MVP metrics.

The MVP does not require:

customer identity profiles

customer accounts

behavioral profiling

heatmaps

advanced attribution

marketing automation

complex tracking infrastructure


Analytics exist to answer a simple question:

> Are people viewing and interacting with the storefront?




---

24. Analytics Reliability Principle

Analytics should not be allowed to break the primary customer journey.

If an analytics event cannot be recorded because of a temporary failure, the storefront should remain usable.

Conceptually:

Customer Action
      ↓
Primary Action
      │
      └── Analytics Recording
               │
               └── Failure must not unnecessarily
                   break the customer experience

Analytics are supporting functionality, not the primary purpose of the storefront.


---

25. QR Code Architecture

The QR code points to the public storefront URL.

Example:

QR Code
   ↓
https://yourapp.com/ada-bakes
   ↓
Business Storefront

It must not point directly to WhatsApp.

This keeps the storefront as the central destination.

The QR code should remain useful even if the storefront's internal experience evolves.


---

26. Digital Business Card Architecture

The digital business card is a generated/available business asset.

It should contain relevant approved business information and the storefront QR code.

Conceptually:

Business Data
     ↓
Business Card Layout
     ↓
QR Code
     ↓
Digital Business Card Asset

It is a supporting feature, not a separate design platform.

The implementation should avoid introducing unnecessary graphic-design infrastructure.


---

27. Preview Architecture

The admin must be able to inspect a business before publishing it.

Conceptually:

Draft Business
      ↓
Preview
      ↓
Admin Reviews
      ↓
Publish

Preview behavior must not accidentally expose unpublished content publicly.

The architecture should distinguish:

Admin Preview

from:

Public Published Storefront


---

28. Publishing Architecture

Publishing changes the public availability of a business.

Conceptually:

Draft
  ↓
Preview
  ↓
Published

A published business can later become:

Published
   ↓
Unpublished

Unpublishing must preserve its data.

Deletion is a separate destructive operation.


---

29. Public Data Retrieval

The public storefront should retrieve only the data necessary to render the public business experience.

Conceptually:

Public Request
      ↓
Business Slug
      ↓
Published Business
      ↓
Public Business Data
      ↓
Related Public Products
      ↓
Storefront

The public request must not receive unrestricted administrative records merely because the application can technically query them.


---

30. Admin Data Retrieval

Administrative operations may require broader access than public storefront rendering.

Conceptually:

Authorized Admin
      ↓
Admin Operation
      ↓
Protected Data Access
      ↓
Supabase

The exact authorization and database access policies belong in DATABASE.md.


---

31. Error Architecture

The application must handle expected failures deliberately.

Important categories include:

invalid URL

non-existent business

unpublished business

missing product

failed data request

failed image upload

invalid admin input

network failure

unauthorized access

failed analytics recording


The application must not expose unnecessary internal technical information to customers.

Customer-facing errors should be understandable.

Administrative errors should provide enough information for the admin to understand what action failed and what can be done next.


---

32. Not-found Handling

A requested business that does not exist must produce a proper not-found experience.

Conceptually:

Requested Business
       ↓
Does it exist?
   ┌───┴───┐
  Yes      No
   ↓        ↓
Storefront Not Found
            Page

The application must not display another business when a requested slug is invalid.

This is a critical isolation requirement.


---

33. Loading Architecture

The application must provide appropriate loading feedback where data retrieval or operations take noticeable time.

Important areas include:

public storefront loading

admin business lists

business editing

product management

image uploads

analytics


Loading states must not falsely imply that an operation has completed when it has not.


---

34. Empty-State Architecture

Empty data is not necessarily an error.

Examples:

No businesses
No products
No analytics
No optional social links
No delivery information

The interface should communicate these states appropriately.

An empty state must not cause broken layouts or confusing blank areas.


--
