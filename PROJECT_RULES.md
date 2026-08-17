# Business Storefront — Project Rules

**Project:** Business Storefront  
**Document:** Project Rules  
**Version:** 1.0  
**Status:** Approved Development Rules  
**Applies To:** ChatGPT, Kiro, Windsurf, v0, future developers, and any other development agent or tool interacting with the project

---

# 1. Purpose

This document defines the mandatory rules for designing, developing, testing, reviewing, modifying, and maintaining the Business Storefront project.

These rules exist to ensure that:

- The approved MVP remains within scope.
- AI coding agents do not make uncontrolled product decisions.
- Security is treated as a requirement.
- The codebase remains understandable and maintainable.
- The project remains portable between development tools.
- Changes are deliberate and reviewable.
- The application is tested before being considered complete.
- The GitHub repository remains the permanent project source of truth.

These rules apply throughout the entire project lifecycle.

---

# 2. Source-of-Truth Hierarchy

The repository documentation must be treated as the project's authoritative reference.

## 2.1 Product Requirements

`PRODUCT_SPEC.md`

Defines:

- What the product is.
- Who it serves.
- What the MVP must do.
- What is explicitly outside the MVP.
- The required customer and admin behavior.
- The MVP acceptance criteria.

If implementation conflicts with the product specification, the conflict must be identified and resolved deliberately.

## 2.2 Project Rules

`PROJECT_RULES.md`

Defines:

- How the project must be developed.
- How AI agents and developers must behave.
- How changes must be controlled.
- Required quality and security practices.

## 2.3 Technical Architecture

`ARCHITECTURE.md`

Defines:

- How the approved product requirements are technically implemented.
- Application structure.
- Technology responsibilities.
- Runtime and deployment relationships.
- Important architectural boundaries.

## 2.4 Database Design

`DATABASE.md`

Defines:

- Database structure.
- Relationships.
- Constraints.
- Data integrity requirements.
- Database security decisions.
- Storage-related database decisions.

## 2.5 Source Code

The actual source code must remain consistent with the approved documentation.

No AI tool, generated response, temporary prototype, or conversation history may silently override repository documentation.

If documentation and implementation disagree, the disagreement must be identified and resolved deliberately.

---

# 3. Core Development Principle

The project follows this principle:

> Build the smallest thing that genuinely works, verify it aggressively, protect it carefully, and only then make it bigger.

The objective is not to maximize the number of features.

The objective is to make the approved MVP:

- Reliable
- Understandable
- Secure
- Maintainable
- Mobile-friendly
- Useful to real businesses

---

# 4. No Uncontrolled Building

AI agents must not blindly generate the entire application in one uncontrolled operation.

Development must happen incrementally.

The preferred development cycle is:

```text
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

Each meaningful feature should be implemented and verified before moving to the next major feature.

An agent must not assume that a large amount of generated code is equivalent to a completed product.


---

5. Do Not Invent Product Requirements

AI agents must not invent product requirements.

An agent must not add a feature merely because:

It seems useful.

It is common in similar applications.

Another application has it.

The AI considers it a best practice.

It is technically easy to implement.

It would make the application appear more advanced.


If a feature is not required by the approved MVP documentation, it should normally be deferred.

If an agent believes an additional feature is important, it must be proposed for review rather than silently implemented.


---

6. MVP Scope Protection

The MVP scope defined in PRODUCT_SPEC.md must be protected.

Features explicitly outside the MVP must not be added during MVP development unless the project owner deliberately approves a scope change.

This includes, but is not limited to:

Client dashboards

Client accounts

Customer accounts

Staff accounts

Online payments

Payment gateways

E-commerce checkout

Inventory management

POS functionality

CRM functionality

Delivery tracking

WhatsApp Business API

WhatsApp automation

AI chatbots

Customer databases

Email marketing

Advanced analytics

Custom domains

Advanced SEO management

Automated business onboarding

Multi-admin permissions

Staff roles

Complex order management

Automated order processing

Subscription systems


Technical possibility is not sufficient justification for adding an out-of-scope feature.


---

7. Product Decisions Require Human Approval

AI agents may recommend solutions.

AI agents must not independently make significant product decisions that alter the approved MVP.

Examples include:

Adding major features

Removing required features

Changing the customer journey

Changing the business model

Changing user roles

Introducing payments

Introducing customer accounts

Changing the purpose of WhatsApp integration

Changing the MVP success criterion

Changing the approved technology direction

Changing the data model in a way that affects product behavior


Such changes require deliberate project-owner approval.


---

8. Approved Technology Direction

The current approved technology direction is:

Responsibility	Technology

Application	Next.js
Database	Supabase
Authentication	Supabase Auth
Image Storage	Supabase Storage
Source Control	GitHub
Primary Builder	Kiro
Secondary Builder	Windsurf
UI Assistance	v0
Cloud Development Environment	GitHub Codespaces
Production Hosting	Render
Rapid Prototyping / Independent Projects	Hostinger Horizons
Product / Architecture Intelligence	ChatGPT


These tools have defined responsibilities.

An AI agent must not silently replace an approved technology with another technology simply because it is convenient.

Any significant technology change must be reviewed before implementation.


---

9. Tool Boundaries

9.1 ChatGPT

ChatGPT is responsible primarily for:

Product reasoning

Planning

Architecture review

Requirements clarification

Technical reasoning

Troubleshooting

Testing strategy

Security review

Quality control

Scope control

Code review assistance


ChatGPT is not the project's source of truth.

The repository is.

9.2 Kiro

Kiro is the primary application development environment.

Kiro should implement approved requirements and technical plans.

Kiro must follow:

PRODUCT_SPEC.md

PROJECT_RULES.md

ARCHITECTURE.md

DATABASE.md

Applicable project-specific instructions


Kiro must not independently expand the MVP.

9.3 Windsurf

Windsurf is the secondary development environment.

It may be used when:

Kiro reaches a usage limitation.

A second development environment is useful.

A second coding perspective is required.

The project owner chooses Windsurf for a task.

A particular task is more convenient to perform there.


Windsurf must work from the existing GitHub project.

Switching from Kiro to Windsurf must not require rebuilding the application from the beginning.

9.4 v0

v0 is primarily used for:

UI exploration

Visual design

Interface concepts

Component concepts

Responsive design exploration


v0 must not independently redefine the application's backend architecture.

A visual concept produced by v0 is not automatically production-ready.

9.5 GitHub

GitHub is the permanent source of truth for the project.

It stores:

Application source code

Project documentation

Project history

Approved configuration that is safe to commit

Version history


No AI development tool owns the project.

9.6 GitHub Codespaces

Codespaces is a development workspace.

It is not:

The application's production host

The application's database

The project's permanent source of truth


The project must remain recoverable from GitHub.

9.7 Supabase

Supabase is responsible for approved backend services, including:

Database

Authentication

Image/file storage

Required backend functionality


Database access and security must follow the approved architecture and database documentation.

9.8 Render

Render is the approved production hosting platform for the main application.

The intended production relationship is:

GitHub
   ↓
Render
   ↓
Live Application
   ↓
Supabase

Render must not be treated as the database.

9.9 Hostinger Horizons

Hostinger Horizons is not part of the required production pipeline for the main Business Storefront MVP.

Its approved role includes:

Rapid prototypes

Independent experiments

Small standalone websites

Quick client projects

Demonstrations

Testing ideas before committing them to the main product


A Horizons prototype must not automatically become the architecture of the main application.

If an idea developed in Horizons proves valuable, it must be deliberately reviewed and, if appropriate, implemented within the approved main architecture.


---

10. GitHub Is the Permanent Project Home

The project must remain portable between development environments.

The following must be possible:

Kiro
  ↓
GitHub
  ↓
Windsurf

or:

Windsurf
  ↓
GitHub
  ↓
Kiro

Switching development tools must not require rebuilding the application from scratch.

Important project knowledge must therefore live inside the repository rather than only inside an AI conversation.


---

11. Documentation Is Part of the Project

Important architectural and development decisions must be documented.

The repository should contain, at minimum:

README.md
PRODUCT_SPEC.md
PROJECT_RULES.md
ARCHITECTURE.md
DATABASE.md

Kiro-specific instructions and steering documentation may exist under:

.kiro/

Documentation must be updated when a major approved architectural decision changes.

Documentation must not be changed casually to make an implementation appear compliant.

If implementation changes first, the documentation must be reviewed and updated deliberately.


---

12. Read Before Modifying

Before making a significant change, an AI coding agent must first inspect the relevant existing project structure and documentation.

An agent must not assume that:

A file does not exist.

A feature has not already been implemented.

A database table does not exist.

A dependency is missing.

A route does not exist.

A previous implementation is safe to replace.


Existing code must be understood before being modified.

Relevant documentation must be consulted before architectural or database changes.


---

13. Preserve Existing Working Functionality

When implementing a new feature, existing working functionality must be preserved unless the change deliberately requires modification.

An agent must avoid unnecessary rewrites.

Do not replace working code merely because a different implementation is preferred.

Prefer:

> Small targeted change



over:

> Unnecessary large rewrite




---

14. Minimal Change Principle

For every task:

> Change only what is necessary to correctly complete the approved task.



Avoid:

Unrelated refactoring

Unnecessary dependency additions

Unnecessary file restructuring

Unrelated UI redesigns

Unrelated database changes

Rewriting stable components without a reason


A larger change must have a clear justification.


---

15. Dependency Discipline

New dependencies must not be added automatically.

Before adding a dependency, determine:

1. Why it is required.


2. Whether the existing stack can already solve the problem.


3. Whether a simpler implementation is possible.


4. Whether it introduces security concerns.


5. Whether it increases application size or complexity.


6. Whether it introduces unnecessary maintenance.



If a dependency is not necessary, do not add it.


---

16. Security Is Mandatory

Security is not an optional enhancement.

Security must be considered during:

Database design

Authentication

Authorization

File uploads

Public routes

Admin routes

Environment configuration

Analytics

Deployment

Error handling


The fact that the application is an MVP does not justify knowingly introducing avoidable security weaknesses.


---

17. Authentication and Authorization

Authentication and authorization are different concerns.

The system must not assume:

> If someone is logged in, they can do everything.



Administrative actions must be protected by appropriate authorization.

The public must not gain administrative access simply by:

Discovering an admin URL

Calling an exposed endpoint

Manipulating a request

Accessing database data directly


Authentication must not be treated as a substitute for authorization.


---

18. Secrets and Credentials

The following must never be committed to GitHub:

Passwords

API secrets

Private keys

Service-role secrets

Authentication secrets

Private tokens

Production credentials

Other sensitive credentials


Sensitive configuration must be provided through appropriate environment configuration.

Agents must inspect .gitignore and environment handling before introducing sensitive configuration.

If a secret is accidentally exposed, development must stop long enough to assess and remediate the exposure appropriately.


---

19. Environment Variables

Environment variables must be used appropriately for sensitive or environment-specific configuration.

Do not hard-code private credentials into application source code.

When adding an environment variable:

1. Use the correct variable name.


2. Document its purpose where appropriate.


3. Ensure secrets are not committed.


4. Ensure the application handles missing configuration clearly.


5. Ensure production configuration is not accidentally exposed to the public client.



Public client-side environment variables must never contain server-only secrets.


---

20. Public and Private Data

The application must maintain a clear separation between:

> Public storefront information



and:

> Private administrative information



Public information may include approved storefront content.

Private information includes:

Admin credentials

Authentication information

Private analytics

Internal administrative data

Security information

Secrets

Private configuration

Internal system information


Public visitors must not receive private information simply because it exists in the database.


---

21. Database Security

Database access must follow the approved security model.

Do not create unrestricted public database access merely to make the application easier to build.

Database security rules must be deliberate.

Any change affecting:

Tables

Relationships

Access policies

Authentication

Storage permissions

Public/private data


must be reviewed carefully.

Where the architecture requires database-level authorization policies, those policies must be implemented and tested rather than relying only on frontend restrictions.


---

22. Database Changes Require Care

Database changes can affect existing application behavior.

Before changing the database, determine:

What currently depends on the affected structure.

Whether existing data could be affected.

Whether the change is required.

Whether the change is reversible.

Whether security policies must also change.

Whether application code must be updated.

Whether storage or related records are affected.


Do not casually delete or rename database fields used by existing functionality.

Destructive schema changes require deliberate review.


---

23. Data Integrity

The application must preserve relationships between businesses and their products.

A product must belong to the correct business.

One business's products must never appear on another business's storefront because of:

An incorrect query

A missing filter

An authorization mistake

An incorrect relationship

A client-side assumption


Business identifiers and relationships must be handled deliberately.

Database constraints should be used where appropriate to protect data integrity.


---

24. Public URL Safety

Public business URLs must remain reliable.

A business slug must be:

Unique

Readable

URL-safe

Stable

Correctly associated with the intended business


Slug collisions must never cause one business to display another business's storefront.

Changing a slug must be treated as a deliberate operation because existing shared links and QR codes may depend on it.

The application must never rely on an exposed database identifier as the intended public storefront URL.


---

25. Published vs Unpublished Businesses

The publication state must be respected everywhere.

A business marked as unpublished must not accidentally appear as a normal public storefront.

Unpublishing must not delete its data.

Publishing and unpublishing must not accidentally alter:

Products

Business information

Analytics history

Images


Public routing must enforce publication status.


---

26. WhatsApp Scope

The MVP uses WhatsApp deep links.

The MVP does not use the WhatsApp Business API.

Agents must not silently introduce:

WhatsApp API infrastructure

Automated WhatsApp replies

Automated order processing

WhatsApp bots

Background WhatsApp message handling


The intended flow is:

Customer
   ↓
Clicks WhatsApp
   ↓
WhatsApp opens
   ↓
Message is pre-filled
   ↓
Customer reviews/edits
   ↓
Customer sends

The actual conversation and order handling remain on WhatsApp.


---

27. Content Integrity

The application must represent business information accurately.

The system must not invent:

Prices

Products

Delivery areas

Opening hours

Social accounts

Business claims

Contact information


Missing information must remain missing or use an appropriate empty state.

AI-generated assumptions must never be presented as verified business information.


---

28. Validation

Input must be validated before it is stored or used.

Validation should exist at appropriate boundaries.

Examples include:

Required business information

Product names

Prices

WhatsApp numbers

URLs

Slugs

Publication actions

Image uploads


Validation must not rely solely on the user interface.

Server-side validation must be used where data integrity, authorization, or security requires it.


---

29. Error Handling

Errors must be handled intentionally.

Customers must not see:

Database errors

Stack traces

Internal implementation details

Private configuration

Sensitive debugging information


Instead, customers should receive clear and useful feedback.

Admin users may receive more detailed operational information where appropriate, but sensitive information must still remain protected.

An error must not silently result in incorrect business data.


---

30. Loading and Empty States

Legitimate loading and empty conditions are part of normal application behavior.

The application must appropriately handle situations such as:

No businesses

No products

No analytics

Image loading

Data loading

Image uploading


Empty data must not automatically be treated as an application failure.


---

31. Mobile-First Requirement

Mobile experience is a mandatory MVP requirement.

The public storefront must prioritize:

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
The public storefront must be tested on an actual mobile device before the MVP is considered complete.
32. Performance Discipline
The public storefront should feel fast on ordinary mobile connections.
Avoid unnecessary:
Heavy dependencies
Huge images
Excessive animations
Complex visual effects
Unnecessary external services
Unnecessary JavaScript
Images should be appropriately optimized.
Performance should be treated as part of product quality.
Do not introduce performance-heavy functionality merely because it looks impressive.
33. Accessibility and Usability
The interface should remain usable by ordinary customers without requiring instructions from the admin.
Important controls must:
Have clear labels.
Have usable touch targets.
Remain readable on mobile.
Have meaningful states.
Provide understandable feedback.
Interactive elements must not rely solely on visual appearance to communicate their purpose.
The public storefront should prioritize clarity over decorative complexity.
34. Analytics Discipline
Analytics must remain within the approved MVP scope.
The MVP tracks only the defined useful interactions, including:
Page views
WhatsApp clicks
Instagram clicks
Facebook clicks
TikTok clicks
Product-specific WhatsApp clicks where implemented
Analytics must remain admin-only.
Do not silently introduce:
Customer identity tracking
Behavioral profiling
Advanced attribution
Marketing automation
Heatmaps
Unnecessary personal-data collection
Collect only what is necessary for the approved MVP metrics.
35. Image and File Upload Discipline
Uploaded files must be handled deliberately.
Before accepting an uploaded image, the implementation should consider:
File type
File size
Storage location
Access rules
Naming/path safety
Failure handling
Replacement behavior
An upload failure must not leave the business or product in an inconsistent state.
Image storage permissions must not expose private data unnecessarily.
36. Public Storefront Integrity
A published storefront must accurately correspond to its business record.
The storefront must:
Resolve the correct business.
Respect publication state.
Display only intended public information.
Display the correct products.
Display the correct prices.
Display the correct availability.
Generate the correct WhatsApp destination.
Avoid exposing internal identifiers unnecessarily.
A public route must never be allowed to select another business's data through uncontrolled user input.
37. Admin Safety
Administrative actions that can cause irreversible or significant changes must require appropriate confirmation.
Examples include:
Business deletion
Product deletion
Destructive data changes
The admin interface should make destructive actions visually and behaviorally distinct from ordinary actions.
An agent must not remove confirmation requirements simply to make the UI faster.
38. Testing Is Mandatory
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
39. End-to-End Testing
The MVP must be tested as a complete system, not only as individual screens.
At minimum, test:
Admin Login
    ↓
Create Business
    ↓
Enter Business Information
    ↓
Add Products
    ↓
Preview
    ↓
Publish
    ↓
Open Public URL
    ↓
Browse Storefront
    ↓
Click WhatsApp
    ↓
WhatsApp Opens
    ↓
Message Is Correct
    ↓
Analytics Recorded
The complete flow must work on a real mobile device.
40. Regression Protection
When a feature is changed, previously working functionality must be checked where the change could affect it.
Examples:
Changing business fields may affect the public storefront.
Changing slugs may affect URLs and QR codes.
Changing product fields may affect WhatsApp messages.
Changing publication logic may affect public routing.
Changing analytics logic may affect existing metrics.
Changing database policies may affect both admin and public access.
A fix must not be considered successful if it creates a new regression elsewhere.
41. Git and Commit Discipline
Changes must be committed deliberately.
A commit should represent a coherent change.
Avoid commits containing unrelated modifications.
Commit messages should clearly communicate what changed.
Before committing:
Inspect the changed files.
Confirm no secrets are included.
Confirm no unrelated changes are present.
Confirm the application still matches the approved documentation.
Run appropriate tests or checks where available.
The repository history should remain understandable.
42. Do Not Commit Temporary or Sensitive Artifacts
Do not commit:
Secrets
Password files
Production credentials
Local environment files containing secrets
Temporary debugging artifacts
Unnecessary generated files
Personal files unrelated to the project
Large build artifacts unless deliberately required
Repository cleanliness is part of maintainability.
43. Branch and Change Discipline
When a change is significant, it should be isolated appropriately rather than mixing unrelated work together.
Changes should be reviewed before becoming part of the stable project state.
If working directly on the main branch for a simple documentation change, the change must still be deliberate and verified.
The project must not use branches as a substitute for review.
44. Documentation Consistency
If an approved implementation changes an architectural, database, security, or product decision, the relevant documentation must be reviewed.
At minimum, consider whether the change affects:
PRODUCT_SPEC.md
PROJECT_RULES.md
ARCHITECTURE.md
DATABASE.md
.kiro/ project instructions
README.md
Do not allow documentation to become materially inconsistent with the implementation.
45. Conflict Resolution
If two project documents appear to conflict:
Identify the exact conflict.
Do not silently choose one.
Determine whether the conflict is product, architectural, database, or implementation-related.
Escalate the decision for deliberate project-owner review.
Update the affected documentation after the decision.
Only then implement the resulting change.
An AI agent must not hide a documentation conflict by silently changing one document.
46. Change Control
Before implementing a meaningful change, evaluate:
Is the change required for the MVP?
Does it solve a real user problem?
Does it conflict with PRODUCT_SPEC.md?
Does it conflict with ARCHITECTURE.md?
Does it affect DATABASE.md?
Does it affect security?
Does it affect existing businesses or URLs?
Does it introduce unnecessary complexity?
Can it safely be added later?
Does it require explicit project-owner approval?
If the change is outside the MVP, it should normally be deferred.
47. No Silent Scope Expansion
An AI agent must not silently expand the product.
The following are examples of scope expansion:
Adding a client dashboard
Adding customer accounts
Adding payment processing
Adding inventory
Adding POS features
Adding AI chat
Adding WhatsApp automation
Adding subscriptions
Adding complex order management
If such functionality becomes desirable, it must be treated as a separate product decision or future version.
48. Production Readiness Standard
The application does not need enterprise-level infrastructure during MVP development.
However, the following are not acceptable merely because this is an MVP:
Known avoidable security weaknesses
Unprotected administrative functionality
Exposed secrets
Broken public URLs
Incorrect business/product relationships
Silent data corruption
Unhandled destructive actions
Unreliable WhatsApp links
Broken mobile experience
Known critical errors
MVP means limited scope.
It does not mean careless engineering.
49. Real-World Validation
When the MVP acceptance criteria are satisfied:
STOP BUILDING NEW FEATURES.
The next priority becomes real-world validation.
The product should be tested with approximately 3–5 real Nigerian businesses.
The admin should observe:
What businesses understand immediately.
What businesses find confusing.
What customers interact with.
Where customers hesitate.
Whether WhatsApp ordering is actually used.
Whether businesses value the storefront.
What businesses request next.
Real-world evidence should determine the next product iteration.
50. Definition of Done
A feature is done only when:
The approved requirement is implemented.
Existing relevant functionality remains intact.
Normal behavior works.
Empty behavior works.
Invalid behavior is handled.
Expected failure behavior is handled.
Security behavior has been considered.
Mobile behavior has been tested where relevant.
Documentation is updated when required.
The change is reviewable.
No unrelated scope has been introduced.
The MVP is done when the acceptance criteria in PRODUCT_SPEC.md are satisfied.
51. Final Project Rule
The Business Storefront project follows this rule:
Build deliberately. Change minimally. Verify aggressively. Protect the data. Protect the scope. Keep the project portable. Never let an AI agent silently decide what the product becomes.
The repository is the permanent home of the project.
The approved documentation defines the intended system.
AI agents are implementation assistants, not autonomous product owners.
52. Final Authority
This document is the approved development-rules baseline for Business Storefront MVP v1.
If an implementation decision conflicts with these rules:
The conflict must be identified.
The relevant documentation must be reviewed.
The decision must be resolved deliberately.
The repository must be left in a consistent state.
No AI agent may silently reinterpret these rules.
No AI agent may silently expand the MVP.
No AI agent may knowingly introduce avoidable security or data-integrity weaknesses.
The project owner remains the final authority for intentional product and scope decisions.
# Tool Independence

Development environments and AI coding tools are replaceable.

The application must not depend on Kiro, Windsurf, v0, GitHub Codespaces, ChatGPT, Hostinger Horizons, or any other development tool at runtime.

GitHub is the permanent source of truth for the project.

The application must remain portable between supported development environments.

Changing development tools must not require rebuilding the application from scratch.

A development tool may be preferred for a particular task, but no single AI coding tool is a required dependency of the product.

If a preferred development tool becomes unavailable, reaches a usage limit, becomes unsuitable, or is no longer used, development must be able to continue from the GitHub repository using another suitable environment.

Development-tool changes must not silently change:

- Product requirements
- Application architecture
- Database design
- Security model
- Production infrastructure
- Public URLs
- Existing application behavior
End of Project Rules v1
