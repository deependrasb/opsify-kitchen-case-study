# System Architecture

High-level context diagram for Opsify Kitchen.

## Mermaid

```mermaid
flowchart TB
  subgraph Users["Users"]
    Owner["Owner / Manager"]
    Cashier["Cashier / POS"]
    Waiter["Waiter"]
    Kitchen["Kitchen Staff"]
    Guest["Guest / Diner"]
  end

  subgraph App["Opsify Kitchen Application"]
    Web["Web MVC Application\n(Admin · POS · Kitchen · Waiter · Website)"]
    API["Waiter REST API"]
    PrintBridge["Print Server Bridge\n(ESC/POS)"]
  end

  DB[("MySQL / MariaDB")]

  subgraph Integrations["External Integrations"]
    Pay["Payment Gateways\n(Stripe · PayPal · Razorpay)"]
    Msg["Email / SMS / WhatsApp"]
    OAuth["Google / Facebook OAuth"]
    Einvoice["E-Invoicing\n(ZATCA where applicable)"]
  end

  Printers["Thermal Printers\n(Bill · KOT · Invoice)"]

  Owner --> Web
  Cashier --> Web
  Waiter --> Web
  Waiter --> API
  Kitchen --> Web
  Guest --> Web

  Web --> DB
  API --> DB
  Web --> Pay
  Web --> Msg
  Web --> OAuth
  Web --> Einvoice
  Web --> PrintBridge
  API --> Web
  PrintBridge --> Printers
```

## Narrative

1. Staff and guests access role-appropriate web surfaces.
2. The MVC application persists operational data in MySQL.
3. Waiter companion flows can use REST endpoints in addition to the browser UI.
4. Payments, messaging, OAuth, and e-invoicing are outbound integrations.
5. Printing is delegated to a local ESC/POS bridge that talks to thermal printers.

Static exports: [system-architecture.png](system-architecture.png) · [system-architecture.svg](system-architecture.svg)
