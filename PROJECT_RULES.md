Absolutely. We should treat PROJECT_RULES.md differently from PRODUCT_SPEC.md.

PRODUCT_SPEC.md answers “What are we building?”

PROJECT_RULES.md answers “How must AI agents and developers behave while building it?”

The document below is therefore deliberately strict, but it does not redefine the product. It references PRODUCT_SPEC.md as the product authority and establishes safeguards against uncontrolled AI changes.



PROJECT_RULES.md


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

# 2. Source of Truth Hierarchy

The following hierarchy must be respected.

## 2.1 Product requirements

`PRODUCT_SPEC.md`

This defines what the Business Storefront MVP is supposed to do.

If an implementation conflicts with the product specification, the conflict must be identified and resolved rather than silently ignored.

## 2.2 Project rules

`PROJECT_RULES.md`

This document defines how the project must be developed and how development agents must behave.

## 2.3 Technical architecture

`ARCHITECTURE.md`

This defines how the approved product requirements are technically implemented.

## 2.4 Database design

`DATABASE.md`

This defines the application's data structure, relationships, constraints, and database-related decisions.

## 2.5 Repository source code

The actual implementation must remain consistent with the approved documentation.

No AI tool, generated response, temporary prototype, or conversation history overrides the repository documentation without deliberate approval.

---

# 3. Core Development Principle

The project follows this principle:

> Build the smallest thing that genuinely works, verify it aggressively, protect it carefully, and only then make it bigger.

The goal is not to maximize the number of features.

The goal is to make the approved MVP reliable, understandable, secure, and useful.

---

 ```markdown
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


Such changes require deliberate project-owner approval.


---

8. Approved Technology Direction

The current approved technology direction is:

Application        → Next.js
Database           → Supabase
Authentication     → Supabase Auth
Image Storage      → Supabase Storage
Source Control     → GitHub
Primary Builder    → Kiro
Secondary Builder  → Windsurf
UI Assistance      → v0
Cloud Workspace    → GitHub Codespaces
Production Hosting → Render
Rapid Prototyping  → Hostinger Horizons
Product/Architecture Intelligence → ChatGPT

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


ChatGPT is not the source of truth.

The repository is.

9.2 Kiro

Kiro is the primary application development environment.

Kiro should implement approved requirements and technical plans.

Kiro must follow:

PRODUCT_SPEC.md

PROJECT_RULES.md

ARCHITECTURE.md

DATABASE.md

applicable project-specific instructions


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

The repository should contain:

README.md
PRODUCT_SPEC.md
PROJECT_RULES.md
ARCHITECTURE.md
DATABASE.md

Kiro-specific instructions and steering documentation may exist under:

.kiro/

Documentation must be updated when a major approved architectural decision changes.


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


---

13. Preserve Existing Working Functionality

When implementing a new feature, existing working functionality must be preserved unless the change deliberately requires modification.

An agent must avoid unnecessary rewrites.

Do not replace working code merely because a different implementation is preferred.

Prefer:

Small targeted change

over:

Unnecessary large rewrite


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

Why it is required.

Whether the existing stack can already solve the problem.

Whether a simpler implementation is possible.

Whether it introduces security concerns.

Whether it increases application size.

Whether it introduces unnecessary maintenance.


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




---

20. Public and Private Data

The application must maintain a clear separation between:

Public storefront information

and:

Private administrative information

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

tables

relationships

access policies

authentication

storage permissions

public/private data


must be reviewed carefully.


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


Do not casually delete or rename database fields used by existing functionality.


---

23. Data Integrity

The application must preserve relationships between businesses and their products.

A product must belong to the correct business.

One business's products must never appear on another business's storefront because of an incorrect query, missing filter, or authorization mistake.

Business identifiers and relationships must be handled deliberately.


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


---

25. Published vs Unpublished Businesses

The publication state must be respected everywhere.

A business marked as unpublished must not accidentally appear as a normal public storefront.

Unpublishing must not delete its data.

Publishing and unpublishing must not accidentally alter products or analytics history.


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

Server-side validation must be considered for data that affects application integrity or security.


---

29. Error Handling

Errors must be handled intentionally.

Customers should not see:

Database errors

Stack traces

Internal implementation details

Private configuration

Sensitive debugging information


Instead, customers should receive clear, useful feedback.

Admin users may receive more detailed operational information where appropriate, but sensitive information must still remain protected.


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

The public storefront must be developed mobile-first.

Every major public feature must be checked on an actual mobile device.

Do not consider the storefront complete merely because it looks correct on a desktop development screen.

Particular attention must be paid to:

Text readability

Touch targets

Product cards

WhatsApp buttons

Image sizing

Scrolling

Navigation

Loading behavior

Error messages



---

32. Accessibility and Usability

The application should follow sensible accessibility and usability practices.

At minimum:

Text must remain readable.

Buttons must be clearly identifiable.

Interactive elements must be usable by touch.

Images should have appropriate alternative text where meaningful.

Form controls should have clear labels.

Important actions should not depend solely on color.

Focus behavior should not be unnecessarily broken.

Error messages should explain what needs attention.


Accessibility improvements must not introduce unnecessary complexity.


---

33. Performance

Performance is part of product quality.

Avoid unnecessary:

Large dependencies

Huge images

Heavy animations

Excessive client-side processing

Unnecessary network requests

Unnecessary external services


Public storefront images should be appropriately optimized.

The storefront should remain usable on ordinary mobile connections.


---

34. UI Consistency

The public storefront should maintain a coherent product identity.

Different businesses may have different:

Names

Images

Products

Descriptions

Business information


However, the underlying experience should remain consistent.

Do not allow individual business content to break the general storefront layout.


---

35. UI Changes Require Functional Awareness

Visual changes must not accidentally break functionality.

When modifying the interface, verify that important actions remain functional, especially:

WhatsApp buttons

Product actions

Navigation

Forms

Publish/unpublish controls

Image uploads

Admin actions

Public URLs


A visually improved screen that breaks functionality is not an improvement.


---

 36. Forms
Forms must provide:
Clear labels
Appropriate input types
Validation
Useful error messages
Clear save/submit actions
Appropriate loading states
Protection against accidental destructive actions
Users should understand whether an action:
Saved successfully
Failed
Is still processing
37. Destructive Actions
Destructive actions must be treated carefully.
Examples:
Delete business
Delete product
Remove important data
Destructive actions should require explicit confirmation.
The confirmation should make the consequence clear.
Do not hide destructive behavior inside ambiguous buttons.
38. Analytics Rules
Analytics must remain within the approved MVP scope.
The MVP requires basic interaction metrics.
Agents must not silently introduce a sophisticated tracking system.
Do not collect unnecessary personal information merely because an analytics tool makes it technically possible.
Analytics should collect only what is necessary for the approved product metrics.
39. Analytics Integrity
Analytics events must correspond to real application actions.
For example:
page_view
whatsapp_click
instagram_click
facebook_click
tiktok_click
An event must not be recorded merely because a component rendered unless that behavior is intentionally defined as the event.
Analytics must not interfere with the main customer experience.
If analytics fail, the storefront should preferably remain usable.
40. Image Handling
Images must be handled deliberately.
Agents must consider:
File type
File size
Upload failures
Missing images
Replacement behavior
Storage permissions
Public display requirements
Performance
Do not allow unrestricted file uploads without appropriate validation and controls.
41. QR Code Integrity
QR codes must point to the business storefront URL.
They must not point directly to WhatsApp for the MVP.
Before considering QR functionality complete, verify:
The QR code is generated correctly.
It points to the intended storefront.
Scanning it on a real mobile device works.
The destination corresponds to the correct business.
The QR code does not expose private information.
42. Digital Business Card Integrity
The digital business card must use the actual business information.
It must not invent content.
Verify:
Business name
Relevant description
Location
QR code
Storefront destination
The digital business card is a useful business asset, not a replacement for the storefront.
43. Testing Is Mandatory
A feature is not considered complete merely because:
The code compiles.
The page appears.
The AI agent says it works.
The browser does not immediately show an error.
A meaningful feature must be tested.
44. Minimum Feature Testing
For major functionality, test:
Normal behavior
The intended action works.
Empty behavior
The feature behaves correctly when data is absent.
Invalid behavior
Invalid information is rejected appropriately.
Failure behavior
Expected network, database, upload, or service failures produce useful feedback.
Mobile behavior
The feature works on a real mobile device.
Security behavior
Unauthorized users cannot access protected functionality or data.
45. End-to-End Testing
Before MVP completion, verify the complete journey:
Admin Login
    ↓
Create Business
    ↓
Enter Information
    ↓
Upload Images
    ↓
Add Products
    ↓
Set Prices
    ↓
Set Availability
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
Verify Message
    ↓
Send Message
    ↓
Check Analytics
    ↓
Unpublish
    ↓
Verify Public Access Is Disabled
    ↓
Republish
    ↓
Verify Public Access Returns
The journey must be tested on a real mobile device before final MVP approval.
46. Regression Testing
When fixing or modifying one feature, verify that important existing features still work.
For example, after changing the public storefront, recheck:
Business URL
Product display
Product availability
WhatsApp buttons
Social links
QR code destination
A new change must not silently break an existing feature.
47. Build and Runtime Verification
Before considering a development milestone complete, verify the project through the appropriate development checks.
At minimum, where applicable:
Project starts successfully.
Application builds successfully.
Relevant tests pass.
No obvious runtime errors remain.
Important routes work.
Important user actions work.
An AI agent must not claim a task is complete without appropriate verification.
If something could not be tested, that limitation must be stated clearly.
48. No False Completion Claims
AI agents must not state:
"Done"
or:
"Everything works"
unless the relevant work has actually been implemented and appropriately verified.
If a test was not performed, say so.
If a result is uncertain, say so.
Accuracy is more important than appearing confident.
49. Explain Uncertainty
When an agent encounters uncertainty, it must not silently guess when the decision could materially affect the project.
Examples:
Ambiguous product behavior
Unclear database relationship
Unclear security requirement
Conflicting documentation
Unclear API behavior
Potential breaking change
The correct response is to identify the uncertainty and seek deliberate resolution.
50. No Silent Architecture Changes
AI agents must not silently change:
Framework
Database
Authentication system
Storage system
Hosting platform
Core routing strategy
Major application architecture
because another solution appears easier.
Architecture changes require review.
51. No Silent Database Changes
Database changes must be deliberate.
An agent must not casually:
Drop tables
Delete fields
Rename fields
Change relationships
Remove security policies
Change access rules
without understanding the consequences and updating the relevant documentation when necessary.
52. Documentation Synchronization
When an approved architectural change occurs, the appropriate documentation must be updated.
Examples:
Architecture change:
ARCHITECTURE.md
Database change:
DATABASE.md
Product requirement change:
PRODUCT_SPEC.md
Development rule change:
PROJECT_RULES.md
Documentation must not intentionally describe an architecture that the code no longer follows.
53. Git Discipline
Meaningful work should be committed in logical increments.
Avoid one enormous commit containing unrelated changes.
Commit messages should clearly describe the change.
Examples:
Add admin authentication
Add business management
Add product management
Add public storefront
Add WhatsApp ordering
Add storefront analytics
The exact wording may vary, but commits should remain understandable.
54. Review Before Commit
Before committing a significant change, review:
What changed?
Why did it change?
Does it satisfy the intended requirement?
Did unrelated files change?
Did security-sensitive files change?
Did database behavior change?
Did existing functionality break?
Was the change tested?
Do not blindly commit generated AI changes.
55. Avoid Unnecessary Repository Noise
Do not commit unnecessary files such as:
Temporary test files
Local secrets
Debug output
Generated caches
Personal configuration
Unnecessary build artifacts
Large temporary assets
Repository contents should remain intentional and clean.
56. AI-Generated Code Must Be Reviewed
AI-generated code is not automatically correct.
Every generated implementation must be treated as code that requires review.
Pay particular attention to:
Authentication
Authorization
Database access
File uploads
User input
Public/private data
Environment variables
Routing
Analytics
Error handling
57. Do Not Optimize Prematurely
Do not introduce complex optimization systems before there is a demonstrated need.
The MVP should prioritize:
Correctness
Security
Reliability
Simplicity
Maintainability
Performance
Future scalability
The application should remain simple enough to understand.
58. Do Not Over-Engineer the MVP
Avoid introducing enterprise-level complexity without a real requirement.
Examples include unnecessary:
Microservices
Complex event systems
Multiple databases
Large infrastructure layers
Unnecessary queues
Unnecessary third-party services
Complex permission systems
The MVP should use the simplest architecture that safely satisfies the approved requirements.
59. Future-Proof Without Future-Building
The project should be structured cleanly enough to support future development.
However:
Designing for future possibilities does not mean implementing future features now.
The correct approach is:
Clean foundation
      ↓
Working MVP
      ↓
Real users
      ↓
Real feedback
      ↓
Validated need
      ↓
Future feature
Do not build speculative features simply because they might be useful later.
60. Real-World Validation
When the MVP satisfies its acceptance criteria, development should shift toward real-world validation.
The initial validation target is approximately:
3–5 real Nigerian businesses
Observe:
What businesses understand immediately
What businesses find confusing
What customers interact with
Where customers hesitate
Whether WhatsApp ordering is used
Whether businesses value the storefront
What businesses request next
Real evidence should guide Version 2.
61. Feedback Must Not Automatically Become a Feature
A customer or business request is evidence, not an automatic requirement.
Before adding requested functionality, evaluate:
How many users need it?
What problem does it solve?
Is the problem important?
Does it fit the product?
Does it belong in the current version?
What complexity does it introduce?
Can it be solved more simply?
A request should be evaluated before implementation.
62. Change Control
Before making a significant change, ask:
Is it required for the MVP?
Does it solve a real user problem?
Does it conflict with PRODUCT_SPEC.md?
Does it affect security?
Does it affect the database?
Does it affect existing businesses?
Does it affect public URLs?
Does it affect analytics?
Does it introduce unnecessary complexity?
Can it safely be postponed?
If the change is outside the MVP, it should normally be deferred.
63. Stop Condition
The MVP has a deliberate stopping point.
Once the approved MVP acceptance criteria are satisfied:
STOP BUILDING NEW FEATURES.
Do not continue adding features simply because development is going well.
Move to:
REAL BUSINESSES
      ↓
REAL CUSTOMERS
      ↓
REAL USAGE
      ↓
MEASURE
      ↓
LEARN
      ↓
DECIDE
      ↓
VERSION 2
64. Final Project Authority Rule
The Business Storefront project must remain controlled, reviewable, and portable.
The fundamental rules are:
PRODUCT_SPEC.md
        ↓
Defines what we build

PROJECT_RULES.md
        ↓
Defines how we build it

ARCHITECTURE.md
        ↓
Defines how the system is structured

DATABASE.md
        ↓
Defines how application data is structured

GitHub
        ↓
Stores the actual project
AI agents are development assistants.
They are not the owners of the product.
They must not silently redefine the product, architecture, security model, database, or scope.
When uncertainty exists:
STOP
  ↓
IDENTIFY THE UNCERTAINTY
  ↓
REVIEW THE DOCUMENTATION
  ↓
ANALYZE THE OPTIONS
  ↓
MAKE A DELIBERATE DECISION
  ↓
DOCUMENT IMPORTANT CHANGES
  ↓
IMPLEMENT
  ↓
TEST
The project prioritizes correctness over speed, simplicity over unnecessary complexity, security over convenience, and verified behavior over assumptions.
65. Final Development Principle
Do not build what we merely can build. Build what we have deliberately decided to build, make it work correctly, verify it, protect it, and only then expand it.
End of Project Rules v1
