# Project Overview — Opsify Kitchen

## Summary

Opsify Kitchen is a restaurant POS and operations platform delivered as a privately hosted web application. It connects front-of-house sales, kitchen fulfilment, inventory and purchasing, guest ordering channels, and management reporting under one multi-outlet model.

This document frames the **business context and delivery scope** for clients evaluating similar platforms or custom restaurant-system work.

---

## Problem Statement

Independent and multi-outlet restaurants commonly face:

1. **Operational fragmentation** — POS, kitchen tickets, inventory, and online orders live in different tools (or on paper).
2. **Slow service handoffs** — Waiters, cashiers, and kitchen staff lack a shared live view of order state.
3. **Weak cost control** — Ingredient usage, waste, and purchasing are hard to reconcile with sales.
4. **Channel sprawl** — Dine-in, takeaway, delivery, and QR/online orders require duplicate processes.
5. **Limited management insight** — Daily sales, tax summaries, and kitchen performance are inconsistent across outlets.

---

## Target Users

| Persona | Primary needs |
|---------|----------------|
| **Restaurant owner / manager** | Multi-outlet oversight, reports, settings, staffing, margins |
| **Cashier / POS operator** | Fast order entry, payments, refunds, register discipline |
| **Waiter** | Table/service orders, notifications, status updates |
| **Kitchen / chef** | Clear tickets by kitchen station, cooking status updates |
| **Guest / diner** | Online menu, self-order via QR, reservations, order status |
| **Back-office / stock role** | Ingredients, purchases, transfers, waste, suppliers |

---

## Solution Scope

### In scope (product capability)

- Role-based access for staff and outlet-scoped operations
- POS sales with register open/close controls
- Kitchen and waiter operational panels
- Menu, modifiers, tables/areas, promotions
- Inventory, purchasing, expenses, customers
- Online ordering website, QR self-order, reservations
- Payment gateway integrations for guest checkout
- Thermal printing for bills and kitchen tickets
- Multilingual UI and white-label branding
- Regional e-invoicing support where configured
- REST-style waiter API for mobile/helper clients
- Operational and financial reporting suite

### Out of scope for this public showcase

- Production source code and private repositories
- Live credentials, keys, and infrastructure hostnames
- Real customer, order, or staff personal data
- Proprietary cryptographic/e-invoice signing implementation details
- Client-specific commercial contracts or SLAs

---

## Delivery Model

Opsify Kitchen is presented here as a **delivered operations platform case study**:

- Deployed as a classic PHP MVC web application on standard LAMP/WAMP-style hosting
- Configured per company/outlet with branding, tax, payment, and messaging settings
- Extended through integrations (payments, messaging, printing, e-invoicing) rather than requiring a separate microservice mesh for core ops

The public materials emphasize **product capability, architecture clarity, and engineering judgement**—not redistribution of commercial application binaries or source.

---

## Business Workflows Supported

```text
Guest / Cashier places order
        │
        ├─► Kitchen panel (prepare)
        ├─► Waiter panel (serve / notify)
        ├─► Print bridge (KOT / bill)
        └─► Inventory & reporting impact
                │
                ▼
        Manager reviews sales, stock, performance
```

Additional channels (online order, QR self-order, reservation) feed into the same operational core so staff do not maintain parallel processes.

---

## Outcomes

Successful deployments of this class of system typically yield:

- Shorter order-to-kitchen latency and fewer missed tickets
- Clearer accountability via roles, registers, and audit-friendly reporting
- Better ingredient and purchase visibility
- Incremental revenue from digital ordering without a second stack
- A consistent brand experience across outlets via white-label settings

Exact KPIs vary by restaurant size, outlet count, and adoption of online/self-order channels.

---

## Related Documents

- [README.md](README.md) — Client-facing case study home
- [FEATURES.md](FEATURES.md) — Feature catalogue
- [TECHNICAL_OVERVIEW.md](TECHNICAL_OVERVIEW.md) — Technical architecture
- [architecture/](architecture/) — Diagrams
