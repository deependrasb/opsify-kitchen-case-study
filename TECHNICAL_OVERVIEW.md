# Technical Overview — Opsify Kitchen

High-level technical documentation for evaluators. This describes architecture, major components, integrations, and engineering challenges **without** publishing proprietary source, secrets, or private infrastructure.

---

## 1. Architectural Style

Opsify Kitchen is a **monolithic MVC web application**:

- Server-rendered PHP views for admin, POS, kitchen, waiter, and public website surfaces
- Shared domain models and MySQL persistence
- Session-based staff context (user, role, outlet, company)
- AJAX endpoints for interactive POS / kitchen / waiter behaviour
- Side integrations for payments, messaging, OAuth, e-invoicing, and printing

This style favours deployability on conventional shared or VPS hosting, operational simplicity, and a single source of truth for restaurant data.

```text
Browser clients (Admin | POS | Kitchen | Waiter | Website)
        │
        ▼
HTTP reverse rewrite (Apache / IIS)
        │
        ▼
Front controller → Router → Controllers
        │
        ├─► Models → MySQL
        ├─► Session + access helpers
        ├─► Views / assets
        └─► Libraries → external services & print bridge
```

---

## 2. Major Components & Responsibilities

| Component | Responsibility |
|-----------|----------------|
| **Authentication & session layer** | Staff login (password / PIN patterns), guest session hooks, outlet selection gates |
| **Access control helpers** | Role/admin bypass and function-level permission checks for modules |
| **Sales / POS module** | Order lifecycle, payments at the counter, refunds, invoices, kitchen status hooks |
| **Kitchen module** | Station panels and cooking status updates |
| **Waiter module** | Floor notifications and order assistance UI |
| **Master data modules** | Menus, ingredients, tables, customers, suppliers, payment methods, etc. |
| **Inventory & purchase modules** | Stock movements, waste, production, transfers, purchasing |
| **Reporting module** | Operational and financial report generation |
| **Frontend / website module** | Public menu, cart, checkout, reservations, content pages |
| **Settings & white-label** | Company configuration, branding JSON, channel toggles |
| **REST API layer** | Waiter-oriented endpoints for companion clients |
| **Print server** | Lightweight HTTP bridge posting ESC/POS jobs to local printers |
| **Integration libraries** | Payments, mail, SMS/WhatsApp, social login, QR, e-invoicing |

---

## 3. Frontend Architecture

- **Pattern:** Classic server-rendered MVC templates (not a separate SPA framework)
- **Admin / ops shell:** Shared layout wrapping module views
- **POS & panels:** Dedicated CSS/JS assets for high-density floor UIs
- **Public site:** Website layout with menu, cart, and checkout flows
- **Interactivity:** jQuery + AJAX for live panels and POS actions
- **State:** Primarily PHP sessions; limited file-based transient cart data for some flows
- **Assets:** AdminLTE/Bootstrap-era UI kits, DataTables/Select2-style widgets, charting libraries as needed

**Design implication:** One deployable app serves all roles; UX differentiation is achieved through routes, layouts, and permission gates rather than separate front-end codebases.

---

## 4. Backend Architecture

- **Framework:** CodeIgniter-style MVC (controllers, models, views, helpers, libraries)
- **Domain controllers:** Separated by business area (sales, kitchen, inventory, reports, authentication, frontend, etc.)
- **Persistence:** MySQL via mysqli; soft-delete / live-status patterns common for operational records
- **Cross-cutting concerns:** Pre-controller hooks for site/demo behaviour; helpers for company, white-label, and access checks
- **URL design:** Pretty routes for public ordering, payment, and auth entry points

Business-critical interactive behaviour (especially POS) is concentrated in sales controllers with numerous AJAX actions—typical for mature restaurant POS products iterating on floor UX.

---

## 5. Data & Storage

| Store | Use |
|-------|-----|
| **MySQL / MariaDB** | Primary system of record (users, outlets, sales, kitchen tickets, inventory, companies, roles, notifications, plans, etc.) |
| **File uploads** | Images, attachments, banners, gallery assets |
| **QR / media folders** | Generated codes and static media |
| **Transient files** | Short-lived cart or cache artefacts where used |
| **Application logs / cache** | Runtime diagnostics and framework cache |

No requirement for Redis, search clusters, or object-storage abstractions in the core architecture—keeping the operational footprint hosting-friendly.

---

## 6. Authentication & Authorization

**Staff**

- Credential or PIN-oriented login into server sessions
- Session carries identity, role, outlet, company, and permission grants
- Most modules require an outlet to be selected
- POS commonly requires an open cash register (with role/channel exceptions)

**Guests**

- Phone/password style sessions for website flows
- Optional Google / Facebook OAuth hooks where configured

**API**

- Waiter REST endpoints accept authenticated waiter credentials for companion workflows

**Showcase note:** Production deployments should use hardened secrets management, HTTPS, and modern password hashing policies appropriate to the hosting environment. Specific credential stores and key values are intentionally not documented here.

---

## 7. Integrations

| Integration | Role in the system |
|-------------|--------------------|
| **Stripe / PayPal / Razorpay** | Guest and online payment capture |
| **SMTP / PHPMailer** | Transactional and operational email |
| **SMS providers** | Text notifications |
| **WhatsApp providers** | Messaging via Twilio-style or alternate API configurations |
| **Google / Facebook OAuth** | Guest social login |
| **Google Maps embed** | Location display from company settings |
| **ESC/POS print server** | Local thermal printing for Bill / KOT / Invoice |
| **ZATCA APIs** | Saudi e-invoicing reporting/clearance path |
| **QR generation** | Self-order and related deep links |
| **Excel import/export libraries** | Bulk master-data operations |

Integrations are configuration-driven so the same codebase can serve different markets and payment preferences.

---

## 8. Notable Technical Challenges & Approaches

| Challenge | Approach (high level) |
|-----------|------------------------|
| **Keeping POS, kitchen, and waiter in sync** | Shared sales/kitchen data model + AJAX polling panels instead of mandating websockets |
| **Multiple order channels** | Normalize dine-in, takeaway, delivery, online, and self-order into a common sales pipeline |
| **Multi-outlet operations** | Outlet session context + permission checks across modules |
| **Reliable thermal printing** | Isolate ESC/POS concerns in a dedicated print-server endpoint callable from the app |
| **Regional e-invoicing** | Dedicated configuration and library path for ZATCA Phase-2 submission on relevant sale/refund events |
| **White-label multi-company needs** | Branding and feature flags stored as company-level configuration |
| **Large interactive POS surface** | Dense server-rendered UI with targeted AJAX endpoints for floor speed |
| **Legacy-friendly hosting** | Prefer PHP/MySQL monolith deployable on common shared hosting / VPS stacks |

---

## 9. Engineering Decisions Worth Highlighting

1. **One product, many role UIs** — Reduces integration debt between POS and kitchen systems.
2. **Print bridge separation** — Keeps printer protocols out of the main request/response path where possible.
3. **Channel-agnostic sales core** — Online and QR orders reuse operational fulfilment paths.
4. **Configuration over forks** — Payments, messaging, language, and branding are settings-driven.
5. **API for waiters** — Extends floor ops to companion clients without rewriting the monolith.
6. **Compliance as a module path** — E-invoicing can be enabled for regulated deployments without restructuring core POS.

---

## 10. System Context Diagram

See also:

- [architecture/system-architecture.md](architecture/system-architecture.md) (Mermaid)
- [architecture/application-architecture.md](architecture/application-architecture.md) (Mermaid)
- [architecture/system-architecture.svg](architecture/system-architecture.svg) (static image)

---

## 11. What This Demonstrates

For clients assessing delivery capability, this codebase class demonstrates:

- Full-lifecycle restaurant domain modelling
- Multi-role UX engineering under real floor constraints
- Integration breadth (payments, messaging, printing, compliance)
- Pragmatic architecture choices for reliability and hostability
- Documentation and packaging suitable for confidential commercial delivery (private source, public capability showcase)

---

## Confidentiality

Production source code, credentials, private URLs, customer records, and proprietary implementation details remain private. This document is intentionally architectural and evaluative.
