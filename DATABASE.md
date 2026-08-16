# Business Storefront MVP — Database Specification


I have kept it aligned with the approved MVP and tightened the areas that matter most: security, public/private data, prices, relationships, slugs, analytics, images, deletion behavior, timestamps, and MVP scope.

# Business Storefront MVP — Database Specification

**Product:** Business Storefront  
**Document:** Database Specification  
**Version:** 1.0  
**Status:** Approved MVP Database Baseline  
**Primary Database Platform:** Supabase  
**Primary Storage Platform:** Supabase Storage  
**Authentication Platform:** Supabase Auth

---

# 1. Purpose

This document defines the approved database requirements for the Business Storefront MVP.

It exists to provide a single database reference for:

- ChatGPT
- Kiro
- Windsurf
- Future developers
- Future technical reviewers

The database must support the approved product requirements without introducing unnecessary functionality.

This document defines the required data structures, relationships, integrity rules, security requirements, storage requirements, and database behavior.

It does not replace:

- `PRODUCT_SPEC.md`
- `PROJECT_RULES.md`
- `ARCHITECTURE.md`

If a database implementation conflicts with an approved product requirement, the conflict must be identified and resolved deliberately.

AI coding agents must not silently change the database architecture.

---

# 2. Database Technology

The approved database platform is:

> Supabase

Supabase will provide the MVP with:

- PostgreSQL database
- Supabase Auth
- Supabase Storage
- Row Level Security (RLS)

The database must use PostgreSQL-compatible structures and constraints supported by Supabase.

---

# 3. MVP Database Scope

The MVP requires data for:

1. Businesses
2. Products
3. Analytics events
4. Admin authentication
5. Business and product images through Supabase Storage

The MVP does NOT require database tables for:

- Customers
- Customer accounts
- Orders
- Shopping carts
- Payments
- Subscriptions
- Inventory
- POS
- CRM
- Staff
- Delivery tracking
- WhatsApp conversations
- WhatsApp automation
- Email marketing
- AI conversations
- Client dashboards
- Client analytics
- Multi-admin permissions

These are outside the approved MVP scope.

---

# 4. High-Level Data Structure

The core database relationship is:

```text
BUSINESS
   │
   ├── PRODUCTS
   │
   └── ANALYTICS EVENTS

SUPABASE AUTH
   │
   └── ADMIN USER

SUPABASE STORAGE
   │
   ├── BUSINESS IMAGES
   └── PRODUCT IMAGES

A business can have:

zero or more products

zero or more analytics events


A product belongs to exactly one business.

An analytics event belongs to one business and may optionally reference one product.


---

5. Core Tables

The MVP database contains these application tables:

businesses
products
analytics_events

Supabase Auth manages authentication identities separately.

The application must not create a duplicate custom password/authentication system.


---

6. Businesses Table

The businesses table represents each business managed by the admin.

Required conceptual fields

id
name
slug
category
description
logo_path
cover_image_path
location
delivery_areas
opening_hours
whatsapp_number
phone_number
instagram_url
facebook_url
tiktok_url
publication_status
created_at
updated_at


---

7. Business ID

Each business must have a unique identifier.

Recommended implementation:

> UUID



The ID is an internal database identifier.

It must not be used as the primary public storefront URL.

Example internal ID:

xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Public URLs should use the business slug instead.


---

8. Business Name

name stores the public business name.

Example:

Ada Bakes

Requirements:

Required

Must not be empty

Must be stored as text

Must be displayed exactly as appropriate for the business


The database should reject an empty required business name.


---

9. Business Category

category identifies the business category.

Examples:

Bakery
Fashion
Restaurant
Barbershop
Beauty
Electronics
Retail

Requirements:

Required

Stored as text for MVP flexibility

Must not be empty


The MVP does not require a separate category table.


---

10. Business Description

description contains the short public description of the business.

Example:

Fresh homemade bread and pastries in Lekki, Lagos.

Requirements:

Required for publishing

Stored as text

Public when the business is published


The system must not automatically invent business descriptions.


---

11. Business Slug

slug is the human-readable public identifier for the business.

Example:

ada-bakes

Public URL:

/ada-bakes

Requirements:

Required

Unique

URL-safe

Human-readable

Stable

Case-insensitive in practice

Must not expose the database ID


The database must enforce slug uniqueness.

Application-level checking alone is not sufficient.


---

12. Slug Collision Protection

Two businesses must never have the same effective public slug.

Example:

ada-bakes
ada-bakes

must never represent two different businesses.

If a requested slug already exists, the application must either:

1. generate a different unique slug, or


2. require the admin to resolve the conflict.



The database uniqueness constraint is the final protection against collisions.


---

13. Business Logo

logo_path stores a reference/path to the business logo in Supabase Storage.

The database should store the storage reference.

The actual image binary must not be stored directly inside the PostgreSQL business record.

The logo may be publicly accessible when required by the published storefront.


---

14. Business Cover Image

cover_image_path stores a reference/path to the business cover/hero image in Supabase Storage.

The actual image file belongs in Supabase Storage.

The database stores only the appropriate reference/path.


---

15. Business Location

location stores the public business location.

Example:

Lekki, Lagos

The MVP does not require:

GPS coordinates

maps

route calculation

geolocation tracking


unless deliberately added in a future version.


---

16. Delivery Areas

delivery_areas stores delivery information provided by the business.

Example:

Lekki
Ikoyi
Victoria Island

The exact storage format may be a simple text representation for the MVP.

The database must not invent delivery areas.

The MVP does not calculate:

delivery fees

delivery routes

delivery times

delivery tracking



---

17. Opening Hours

opening_hours stores the business's publicly provided operating hours.

Example:

Monday–Saturday, 8:00 AM–7:00 PM

The MVP does not require:

automated scheduling

appointment booking

calendar integration

automatic business-status calculation


unless deliberately introduced later.


---

18. WhatsApp Number

whatsapp_number stores the business's WhatsApp contact number.

This is a core field because WhatsApp ordering is central to the product.

The stored value must be validated sufficiently to allow reliable WhatsApp link generation.

The application should use an appropriate international phone-number representation where possible.

For Nigerian businesses, the system should correctly support Nigerian numbers.

The database must not store an intentionally malformed value as a valid WhatsApp number.


---

19. Phone Number

phone_number stores an optional public phone number.

It may be different from the WhatsApp number.

It should only appear publicly when provided.


---

20. Social Links

The business record may contain:

instagram_url
facebook_url
tiktok_url

These fields are optional.

If a value is absent, the corresponding public button must not be displayed.

The application must validate that supplied values are appropriate URLs before publication.


---

21. Publication Status

Each business must have a publication state.

Minimum allowed states:

draft
published
unpublished

Recommended implementation:

> Controlled text value or database enum.



The implementation must prevent unsupported publication states.


---

22. Publication State Behavior

Draft

The business is being prepared.

The normal public storefront must not be accessible.

Published

The storefront is publicly accessible.

Unpublished

The storefront is temporarily unavailable publicly, but its data remains available to the admin.

Unpublishing must not delete:

business data

products

images

analytics history


unless a deliberate deletion occurs.


---

23. Business Timestamps

Each business must contain:

created_at
updated_at

created_at records when the record was created.

updated_at records the most recent meaningful modification.

The database design should ensure updated_at is reliably maintained.

Application code must not be the only mechanism responsible for remembering to update it.


---

24. Products Table

The products table represents products or services belonging to businesses.

Conceptual fields:

id
business_id
name
description
price
image_path
availability_status
is_popular
created_at
updated_at


---

25. Product ID

Each product must have a unique internal identifier.

Recommended implementation:

> UUID



The product ID is an internal identifier.

It does not need to appear in the public storefront URL.


---

26. Product-to-Business Relationship

Every product must belong to exactly one business.

Relationship:

businesses.id
      ↓
products.business_id

business_id must be a foreign key referencing the appropriate business record.

A product must never belong to multiple businesses.


---

27. Product Name

name stores the product/service name.

Example:

Agege Bread

Requirements:

Required

Must not be empty

Stored as text



---

28. Product Description

description stores optional additional information about the product/service.

Example:

Freshly baked every morning.

The description must not contain fabricated claims.


---

29. Product Price

price stores the product/service price.

The MVP primarily targets Nigerian businesses and therefore supports Nigerian Naira.

Example displayed value:

₦2,500

The database must not use floating-point representation for monetary values.

A safe integer representation in the smallest relevant currency unit should be used.

For Nigerian Naira, the recommended representation is:

kobo

Example:

₦2,500.00

may be stored as:

250000

if prices are represented in kobo.

The application is responsible for formatting the stored value into a customer-friendly Naira display.

The MVP does not process payments.


---

30. Product Availability

Each product must have an availability state.

Minimum states:

available
unavailable

The database must prevent unsupported states.

Availability can change without deleting the product.

This allows the admin to temporarily mark a product unavailable.


---

31. Product Popular State

is_popular represents whether the admin has marked the product as popular.

Recommended representation:

boolean

Default:

false

Popular status does not affect:

price

availability

ownership

ordering

analytics


It is purely a presentation property.


---

32. Product Image

image_path stores the reference/path to a product image in Supabase Storage.

The actual image binary belongs in Storage, not the database row.

A missing product image must not cause the public storefront to break.

The application must provide an appropriate fallback.


---

33. Product Timestamps

Each product must contain:

created_at
updated_at

These timestamps must follow the same consistency rules as business timestamps.


---

34. Analytics Events Table

The analytics_events table records defined storefront interactions.

Conceptual fields:

id
business_id
product_id
event_type
created_at

The table must remain intentionally simple.


---

35. Analytics Event ID

Each analytics event must have a unique identifier.

Recommended implementation:

> UUID



Analytics events are internal records.

They do not need to be exposed to public customers.


---

36. Analytics Business Relationship

Every analytics event must belong to a business.

Relationship:

businesses.id
      ↓
analytics_events.business_id

The database should enforce the relationship with a foreign key.


---

37. Analytics Product Relationship

product_id is optional.

It is used when an event relates specifically to a product.

Example:

whatsapp_click

on:

Agege Bread

may reference the Agege Bread product.

A business-level WhatsApp click may have no product reference.


---

38. Analytics Event Types

Minimum supported event types:

page_view
whatsapp_click
instagram_click
facebook_click
tiktok_click

The database should prevent arbitrary unsupported event types from being inserted.

New event types may be introduced later through deliberate product/technical review.


---

39. Analytics Timestamps

Each analytics event must contain:

created_at

The timestamp should represent when the event was recorded.

The database should use a timezone-aware timestamp representation.

The system should use UTC for stored timestamps unless there is a deliberate reason to do otherwise.

Display timezone can be handled by the application.


---

40. Analytics Data Minimization

The MVP should collect only information required for the approved analytics metrics.

The analytics system does not need to build a customer identity database.

The MVP does not require storing:

customer names

customer phone numbers

customer email addresses

WhatsApp message contents

customer accounts

detailed behavioral profiles


The goal is basic storefront interaction measurement, not customer surveillance.


---

41. Analytics Retention

The MVP does not require an advanced retention system.

Analytics records should remain available to the admin unless:

the product specification is deliberately changed, or

a documented data-management policy requires removal.


The implementation must not silently delete useful analytics data.


---

42. Business Deletion

Deleting a business is a destructive action.

The admin interface must require explicit confirmation.

The database relationships must be designed deliberately so that deleting a business does not leave broken product relationships.

Products belonging exclusively to a deleted business may be deleted as part of the deliberate business deletion operation.

This behavior must be implemented intentionally and tested.


---

43. Analytics and Business Deletion

Analytics require special consideration because they represent historical information.

The implementation must deliberately decide what happens to analytics when a business is permanently deleted.

For the MVP, the preferred behavior is:

> Business deletion removes the business's associated application data and associated analytics records together.



This prevents orphaned analytics records that reference a business that no longer exists.

This behavior must be implemented through deliberate database relationships or a controlled deletion process.


---

44. Unpublish vs Delete

These operations must remain completely different.

Unpublish

Keeps:

business

products

images

analytics

configuration


but removes the public storefront.

Delete

Permanently removes the business and its dependent application data according to the approved deletion rules.

The application must never treat unpublishing as deletion.


---

45. Referential Integrity

Foreign-key relationships must be used wherever appropriate.

At minimum:

products.business_id
        → businesses.id

analytics_events.business_id
        → businesses.id

analytics_events.product_id
        → products.id

The database must prevent invalid references.


---

46. Product and Analytics Integrity

If a product is deleted, analytics events that reference that product must not become invalid database records.

The implementation must deliberately choose appropriate behavior.

For MVP simplicity, product-specific analytics may be deleted or have their product reference removed while preserving the business-level analytics record, depending on the final database relationship configuration.

The chosen behavior must preserve database integrity and must not produce orphaned foreign-key references.


---

47. Public Storefront Data Protection

The public storefront must expose only intentionally public business information.

Public visitors must not receive:

admin information

authentication information

private analytics

internal configuration

secrets

database management information

unrelated businesses' private data


The database security model must support this requirement.


---

48. Row Level Security

Supabase Row Level Security (RLS) must be enabled for application tables where public or authenticated access exists.

RLS must not be treated as optional.

The purpose is to ensure that database access follows the approved product permissions.

At minimum, the database security model must distinguish between:

PUBLIC VISITOR
ADMIN


---

49. Public Read Access

Public visitors need access to published storefront information.

Public access should be limited to businesses whose publication state is:

published

Public visitors must not be able to read:

draft businesses

unpublished businesses

private analytics

administrative data


unless the architecture deliberately provides another secure mechanism.


---

50. Public Product Access

Public visitors may view products belonging to a published business.

They must not be able to access products belonging to:

draft businesses

unpublished businesses


through the public storefront data path.


---

51. Admin Access

The authenticated admin must be able to perform approved management operations.

These include:

Create businesses

Read businesses

Update businesses

Delete businesses

Create products

Read products

Update products

Delete products

View analytics

Manage approved image references


The database must enforce authorization rather than relying solely on the frontend to hide controls.


---

52. Single Admin Model

The MVP has one authorized admin.

The database must not introduce unnecessary multi-role permission complexity.

However, the design should avoid hard-coding assumptions that make future controlled expansion impossible.

Future staff or multi-admin functionality must be introduced deliberately.


---

53. Authentication

Authentication must use:

> Supabase Auth



The application must not create its own password storage system.

Authentication credentials must not be stored manually inside the application database.

The authenticated user's identity should be used by authorization policies where required.


---

54. Authorization

Authentication answers:

> Who is this user?



Authorization answers:

> What is this user allowed to do?



The database security model must account for both.

An authenticated user must not automatically receive unrestricted access unless that user is authorized as the admin.

The frontend must not be the sole security boundary.


---

55. Secrets

The database must never contain or expose application secrets unnecessarily.

Secrets include:

Supabase service-role keys

private API keys

deployment credentials

private authentication secrets

other sensitive configuration


Secrets must not be committed to GitHub.

They belong in secure environment configuration.


---

56. Supabase Service Role

The Supabase service-role key must never be exposed to the browser or public client-side code.

It must only be used in an appropriately protected server-side environment when required.

Public Supabase configuration must not be confused with secret service credentials.


---

57. Storage Architecture
Supabase Storage is responsible for image files.
The PostgreSQL database stores references to those files.
Conceptually:
Database
   │
   └── image_path
          │
          ↓
Supabase Storage
          │
          └── actual image
The database must not store large image binaries as ordinary business/product fields.
58. Storage Categories
The MVP requires image storage for:
Business logo
Business cover image
Product images
Storage organization should be predictable.
A logical structure may follow:
businesses/{business_id}/logo
businesses/{business_id}/cover
businesses/{business_id}/products/{product_id}
The exact bucket/path naming may be adjusted during implementation, but the organization must remain understandable and maintainable.
59. Storage Security
Storage access must follow the same public/private principles as the database.
Public storefront images may be publicly readable where required.
Administrative/private files must not be publicly exposed.
Upload and deletion permissions must be restricted to the authorized admin.
The frontend must not be trusted as the only security boundary for file operations.
60. Image Replacement
When an image is replaced, the system should avoid leaving unnecessary orphaned files in Storage.
The implementation should deliberately handle:
Upload new image
Update database reference
Remove old image when safe
If an upload fails, the existing valid image reference must not be accidentally destroyed.
61. Image Upload Validation
The application should validate uploaded images before storing them.
At minimum, validation should consider:
File type
File size
Reasonable dimensions
Successful upload
The system should reject obviously unsuitable files.
Exact limits should be chosen during implementation based on the application's performance requirements.
62. Database Constraints
Where practical, important rules must be enforced by the database rather than relying only on application code.
Examples include:
Required fields
Unique business slugs
Valid publication states
Valid availability states
Valid analytics event types
Valid foreign-key relationships
This provides a second layer of protection against incorrect application behavior.
63. Nullability
Optional business information should be allowed to remain absent.
Examples:
phone_number
instagram_url
facebook_url
tiktok_url
delivery_areas
opening_hours
logo_path
cover_image_path
The database must not force fake placeholder values such as:
N/A
None
Unknown
Not provided
when the information was simply not supplied.
The application should handle missing optional values appropriately.
64. Required vs Optional Business Data
The minimum information required before publishing should align with PRODUCT_SPEC.md.
Required for credible publication:
Business name
Category
Description
WhatsApp number
Location
Unique slug
Products require at minimum:
Name
Price
Availability
Image requirements should follow the final product/implementation decision.
The database must not silently invent missing values.
65. Data Validation
Validation should exist at the appropriate layers.
The application should validate user input for usability.
The database should enforce critical integrity constraints.
Neither layer should be treated as a replacement for the other.
Examples:
Application:
Friendly validation messages

Database:
Unique constraints
Foreign keys
Allowed states
Required fields
66. Public Data Model
The public storefront conceptually needs access to:
Business
    name
    category
    description
    logo
    cover
    location
    delivery areas
    opening hours
    WhatsApp
    phone
    social links

Products
    name
    description
    price
    image
    availability
    popular
Only published businesses and their appropriate products should be publicly readable.
67. Private Data Model
Private/admin-only information includes:
Admin authentication
Private analytics
Internal database information
Internal configuration
Secrets
Management operations
The database security model must prevent public visitors from accessing private data.
68. Database Indexing
Indexes should be added where they materially improve expected MVP queries.
At minimum, consideration should be given to:
businesses.slug
businesses.publication_status
products.business_id
analytics_events.business_id
analytics_events.created_at
analytics_events.event_type
Indexes must not be added indiscriminately.
The implementation should favor useful indexes over unnecessary database complexity.
69. Slug Lookup Performance
Because public storefronts are accessed through slugs, the slug lookup must be efficient.
The database should enforce a unique index/constraint on:
businesses.slug
Public storefront lookup should not require scanning the entire business table.
70. Product Lookup Performance
Products will normally be retrieved by:
business_id
Therefore, the database should provide an appropriate index for the relationship.
The public storefront should retrieve only the products belonging to the requested published business.
71. Analytics Query Performance
The admin analytics dashboard may query analytics by:
business_id
event_type
created_at
Appropriate indexing should support these basic queries.
The MVP does not require a separate analytics warehouse or external analytics database.
72. Database Transactions
Operations involving multiple related changes should use appropriate transactional behavior where necessary.
Examples:
Creating a business and required related records
Deleting a business and dependent records
Publishing changes that require multiple consistent updates
The goal is to avoid partially completed operations that leave inconsistent data.
73. Partial Failure Protection
The system must consider failures during:
Business creation
Product creation
Image upload
Image replacement
Business deletion
Product deletion
Analytics recording
A failed operation must not unnecessarily leave the database in a broken state.
For example:
If a new image upload fails, the previous valid image reference should remain intact.
74. Analytics Failure Behavior
Analytics must not break the customer experience.
If recording an analytics event fails:
The storefront should still work.
Analytics are secondary to the core customer journey.
A failure in analytics must not prevent:
viewing products
viewing the business
clicking WhatsApp
opening social links
75. Public Storefront Failure Behavior
If the database cannot load a storefront:
The customer should receive a useful error state.
The application must not expose:
SQL errors
Supabase internal errors
stack traces
secret information
internal database details
76. Database Error Handling
Raw database errors should not normally be displayed directly to customers.
The application should translate expected failures into understandable messages.
Example:
Instead of exposing:
PostgrestError: relation businesses...
the customer should receive an appropriate message such as:
We couldn't load this storefront right now.
Please try again.
77. Data Consistency Rules
The database must maintain these basic truths:
Every product belongs to one business.

Every analytics event belongs to one business.

Every product-specific analytics event references a valid product when product_id is present.

Every public business has a unique slug.

Only supported publication states exist.

Only supported product availability states exist.

Only supported analytics event types exist.
These are fundamental integrity rules.
78. No Duplicate Business Data
The database should avoid unnecessary duplication of the same business information across multiple tables.
For example, product records should reference:
business_id
rather than repeatedly storing the full business name.
This reduces inconsistency.

79. No Duplicate Product Ownership
A product must have one authoritative owner:
business_id
The application must not maintain competing ownership fields that could disagree.
80. Public URL Stability
Changing unrelated business information must not change the public URL.
For example:
Changing:
description
price
location
cover image
must not automatically change:
/ada-bakes
The slug should remain stable unless deliberately changed by the admin through an approved workflow.
81. Slug Changes
The MVP should treat slug changes carefully because existing QR codes and shared links may depend on them.
If slug editing is implemented, the application must deliberately consider:
Existing shared URLs
QR codes
Social posts
Printed materials
The database must not silently change a public slug as a side effect of editing the business name.
82. QR Code Relationship
The QR code does not need a separate database table for the MVP.
The QR code can be generated from:
Public storefront URL
Example:
https://yourapp.com/ada-bakes
The QR code should point to the storefront, not directly to WhatsApp.
This keeps the storefront as the central destination.
83. Digital Business Card Relationship
The digital business card does not require a separate database entity for the MVP.
It can be generated from existing:
Business data
+
Public storefront URL
+
QR code
The generated asset should not require duplicating business data into another database table.
84. Database Does Not Store WhatsApp Conversations
The MVP does not store:
WhatsApp messages
Customer conversations
Customer contact lists
Order histories
WhatsApp remains the external communication channel.
The application only generates the appropriate WhatsApp link/message.
85. Database Does Not Process Payments
The MVP database does not contain payment-processing functionality.
There are no MVP tables for:
transactions
payment methods
invoices
subscriptions
payment gateways
Payment functionality is outside the approved MVP.
86. Database Does Not Implement Inventory
The MVP database is not an inventory database.
The product availability field only indicates whether a product can currently be presented as available.
It does not represent:
stock quantity
warehouse quantity
purchase cost
stock movements
reorder levels
Inventory is outside the MVP.
87. Database Does Not Implement Orders
A WhatsApp click is not an order record.
The MVP must not interpret:
whatsapp_click
as:
confirmed order
The customer and business complete their conversation on WhatsApp.
The database records only the defined analytics interaction.
88. Database Does Not Implement Customer Accounts
There is no customer table in the MVP.
Customers can browse anonymously.
The database must not create customer identities merely because someone visits a storefront.
89. Database Does Not Implement Business Accounts
Business owners do not have application accounts in the MVP.
The admin manually manages business storefronts.
Business-owner authentication is outside the MVP.
90. Backup and Recovery
The production database must use the backup and recovery capabilities provided by the chosen Supabase plan/configuration.
The project should not rely solely on the application source code as a backup of database data.
The database contains information that cannot be reconstructed from GitHub source code.
Database backup/recovery procedures must be reviewed before production use.
91. Migration Management
Database schema changes must be managed deliberately.
AI agents must not make uncontrolled production database changes.
Schema changes should be:
Planned
Reviewed
Implemented through a controlled migration
Tested
Verified
Applied to production deliberately
The project should maintain a clear history of database schema changes.
92. Production Database Rule
The production database is not a playground.
AI agents must not experiment directly against production data.
Development/testing should use an appropriate non-production environment or carefully controlled test data where available.
Production changes require deliberate approval.
93. Seed/Test Data
Test businesses and products may be created for development.
Test data must be clearly distinguishable from real production businesses.
Test credentials and test information must never be presented as real customer/business data.
Before production launch, unnecessary test data should be removed or clearly isolated.
94. Database Environment Separation
Where practical, maintain separation between:
Development
Testing
Production
Production credentials must never be casually copied into development environments.
The project must not commit environment secrets to GitHub.
95. Database Security Review
Before production launch, the database implementation must be reviewed for:
RLS enabled where required
Correct public read behavior
Correct admin write behavior
No public analytics access
No public draft/unpublished business access
No unauthorized product access
Secure Storage policies
No exposed service-role key
Correct foreign keys
Correct unique constraints
Correct allowed states
Correct deletion behavior
96. Database Acceptance Criteria
The database implementation is not considered complete until:
Businesses can be created.
Business slugs are unique.
Products can be linked to businesses.
Products cannot reference nonexistent businesses.
Product prices are stored safely.
Product availability is constrained to supported states.
Popular status works correctly.
Analytics events can be recorded.
Analytics events reference valid businesses.
Product-specific analytics reference valid products.
Public users can access only published storefront data.
Public users cannot access private analytics.
Public users cannot access draft businesses.
Public users cannot access unpublished businesses.
Admin authentication works.
Unauthorized users cannot perform admin operations.
Images are stored in Supabase Storage.
Database records store image references rather than image binaries.
Business deletion does not leave broken product relationships.
Analytics deletion behavior is deliberate and tested.
Timestamps work consistently.
Required database constraints are enforced.
Appropriate indexes exist for primary MVP queries.
Production secrets are not stored in GitHub.
Database migrations are controlled.
The complete database works with the approved application architecture.
97. Database Definition of Done
The database is considered production-ready for the MVP when:
BUSINESSES
    ↓
Can be created, edited, published, unpublished and deleted safely

PRODUCTS
    ↓
Can be created, edited, made available/unavailable and deleted safely

IMAGES
    ↓
Are stored and referenced correctly

ANALYTICS
    ↓
Record approved storefront interactions

SECURITY
    ↓
Public and admin access are properly separated

INTEGRITY
    ↓
Relationships and constraints prevent invalid data

PERFORMANCE
    ↓
Basic storefront and admin queries are efficient

RECOVERY
    ↓
Production data is backed up according to the Supabase setup

MIGRATIONS
    ↓
Schema changes are controlled and traceable
98. Final Database Principle
The database follows this principle:
Store what the MVP genuinely needs, protect what must remain private, enforce important rules at the database level, keep relationships clean, and avoid building future systems before the product requires them.
The database must be:
Simple
Secure
Consistent
Maintainable
Understandable
Appropriate for the MVP
Capable of supporting future deliberate expansion
It must not become unnecessarily complicated simply because more functionality may exist in the future.
99. Authority
This document is the approved database baseline for:
Business Storefront MVP v1
It must be used together with:
PRODUCT_SPEC.md
PROJECT_RULES.md
ARCHITECTURE.md
If an implementation decision conflicts with this document, the conflict must be identified and reviewed before implementation.
AI coding agents must not silently reinterpret, remove, or expand database requirements.
Changes to the database architecture must be deliberate, documented, reviewed, and tested.
End of Database Specification v1
          │
          
