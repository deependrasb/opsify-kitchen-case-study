# Features — Opsify Kitchen

Feature catalogue for the Opsify Kitchen restaurant POS & operations platform. Descriptions are product-level and intentionally omit proprietary implementation detail.

---

## 1. Access, Outlets & Administration

- Staff authentication (email/password and PIN-style floor login patterns)
- Role-based access control for modules and actions
- Multi-outlet selection and outlet-scoped sessions
- User and role management
- Attendance check-in / check-out
- Company settings (tax, operational toggles, messaging, ordering channels)
- White-label branding (site name, logo, favicon)
- Plugin enable/disable controls where available
- Multilingual interface packs

---

## 2. Point of Sale & Sales Operations

- Full POS order entry UI
- Multiple order types (dine-in, takeaway, delivery, and digital channels)
- Hold / suspend and resume workflows
- Split sales support
- Running orders and kitchen status visibility from sales context
- Refunds and invoice generation (including thermal sizes)
- Cash register open / close discipline before POS use (configurable exceptions)
- Payment method configuration and denominations
- Multi-currency support where configured
- Promotion application

---

## 3. Kitchen & Waiter Operations

- Kitchen display panels (optionally by kitchen/station type)
- Cooking status progression for tickets
- Waiter panel for order/notification workflows
- Customer-facing order status / customer display screens
- Waiter-oriented REST API for mobile or companion clients

---

## 4. Menu, Floor & Guest Experience

- Food menus and categories
- Modifiers and pre-made food items
- Tables, areas, and counters; table layout support
- Delivery partner configuration
- Public website: home, menu, item detail, cart/checkout
- About / contact content
- Reservations
- Guest order history and ratings (where enabled)
- QR self-order entry points
- Online order entry points

---

## 5. Inventory & Supply Chain

- Ingredients, categories, and units
- Inventory levels and low-stock awareness
- Inventory adjustments
- Waste recording
- Production workflows
- Inter-outlet or stock transfers
- Purchases and purchase history
- Suppliers and supplier payments
- Excel-oriented import/export for menus, ingredients, and customers (where enabled)

---

## 6. Customers & Commercial Ops

- Customer profiles
- Customer due receive workflows
- Loyalty point reporting
- Expenses and expense items
- Delivery partner coordination for delivery-type orders

---

## 7. Payments & Checkout

- Online checkout flows integrated with major gateways:
  - Stripe
  - PayPal
  - Razorpay
- Payment form and confirmation flows for guest channels
- Configurable payment methods for in-store operations

---

## 8. Printing & Hardware Adjacency

- Thermal printing for Bill, KOT, and Invoice document types
- Dedicated print-server bridge for ESC/POS-compatible printers
- Printer configuration in admin settings

---

## 9. Compliance & Regional Capabilities

- ZATCA Phase-2 e-invoicing path for markets that require it (sale and refund submission patterns)
- VAT / tax-oriented reporting support
- Arabic and other language packs for regional deployments

---

## 10. Reporting & Insights

Representative report areas include:

- Dashboard KPIs (sales signals, top items/customers, order-type mix, low stock)
- Daily / sales summaries
- Purchase reporting
- Profit & loss style summaries
- VAT / tax reports
- Z-report style register summaries
- Kitchen performance
- Audit log style operational history
- Loyalty and other commercial reports

*(Exact report list depends on deployment configuration and role access.)*

---

## 11. Digital Channels & SaaS-Oriented Paths

- Online ordering website and checkout
- QR self-order routes
- Reservation intake
- Optional SaaS-oriented plan / signup / subscription payment routes (availability depends on deployment package and enabled views)

---

## Capability Highlights for Evaluators

These features collectively demonstrate experience delivering:

1. **Complex multi-role UIs** in a single product surface  
2. **Operational realtime-ish sync** between POS, kitchen, and waiter  
3. **Inventory-backed F&B workflows**, not POS-only billing  
4. **Omnichannel order intake** into one sales core  
5. **Payment, messaging, printing, and compliance integrations**  
6. **Multi-outlet and white-label deployment readiness**

---

## Related Documents

- [README.md](README.md)
- [PROJECT_OVERVIEW.md](PROJECT_OVERVIEW.md)
- [TECHNICAL_OVERVIEW.md](TECHNICAL_OVERVIEW.md)
