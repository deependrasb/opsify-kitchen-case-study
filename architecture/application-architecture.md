# Application Architecture

Internal module view of the Opsify Kitchen web application.

## Mermaid — Request Flow

```mermaid
flowchart LR
  Client["Browser / Waiter Client"] --> RW["Web Server Rewrite\n(Apache / IIS)"]
  RW --> FC["Front Controller"]
  FC --> Router["Router"]
  Router --> Ctrl["Domain Controllers"]
  Ctrl --> Models["Models"]
  Models --> DB[("MySQL")]
  Ctrl --> Views["Views / Assets"]
  Ctrl --> Libs["Libraries & Helpers"]
  Libs --> Ext["External Services"]
  Ctrl --> Print["Print Bridge"]
```

## Mermaid — Domain Modules

```mermaid
flowchart TB
  subgraph Core["Core Platform"]
    Auth["Authentication &\nSession / ACL"]
    Outlet["Outlet Context"]
    Settings["Settings &\nWhite-Label"]
  end

  subgraph Ops["Floor Operations"]
    POS["Sales / POS"]
    Reg["Cash Register"]
    Kit["Kitchen Panels"]
    Wait["Waiter Panels"]
    Disp["Order / Customer Display"]
  end

  subgraph BackOffice["Back Office"]
    Menu["Menus & Modifiers"]
    Inv["Inventory & Waste"]
    Purch["Purchases & Suppliers"]
    Cust["Customers & Loyalty"]
    Exp["Expenses"]
    Reports["Reports"]
    Users["Users & Roles"]
  end

  subgraph Channels["Guest Channels"]
    Site["Online Website"]
    QR["QR Self-Order"]
    Res["Reservations"]
    PayFlow["Checkout / Payments"]
  end

  Auth --> Outlet
  Outlet --> POS
  Outlet --> Kit
  Outlet --> Wait
  POS --> Kit
  POS --> Wait
  POS --> Inv
  Site --> PayFlow
  QR --> POS
  Site --> POS
  Auth --> Users
  Settings --> Site
```

## Component notes

| Area | Notes |
|------|--------|
| **Core** | Establishes identity, permissions, outlet scope, and branding |
| **Floor ops** | Latency-sensitive UIs; heavy use of AJAX for status updates |
| **Back office** | Master data and commercial controls feeding POS and reports |
| **Guest channels** | Public routes that create or advance orders in the shared sales core |

No proprietary class names, table schemas, or private endpoints are listed here.
