# BakeBridge 🍞  
_Unified Bakery Management Platform_

BakeBridge is a **full-stack, microservices-based platform** for a single-location Indian bakery.  
It combines:

- 🛒 **Customer E-Commerce Website** – browse, order, pay (UPI / cards), track orders  
- 🧑‍💼 **Admin Portal** – inventory, staff, salaries, marketing, analytics  
- 🧾 **Shop Management / POS Web App** – in-store billing, inventory updates, worker management, offline-first  

All of this runs as one cohesive system, powered by **Spring Boot microservices, a GraphQL BFF, Redis**, and a **React** front-end.

---

## ✨ Core Features

### 1. Customer E-Commerce Website
- Product catalog with categories (cakes, pastries, breads, snacks, etc.)
- Cart, checkout, and order history
- **UPI, card, and net banking payments** via Indian payment gateway
- Delivery / pickup options and advance orders (pre-book for birthdays, events)
- Multi-language UI (e.g., English + regional language)
- Order tracking with live status updates

### 2. Admin Portal
- Product & inventory CRUD (with stock levels and shelf-life / expiry)
- Worker management (roles, contact, active/inactive)
- Salary & basic payroll tracking
- Order & billing overview (online + in-store)
- Discounts, coupons, and offers management
- Marketing tools (SMS / email campaigns, birthday offers, etc.)
- Business analytics dashboard:
  - Sales trends (daily/weekly/monthly)
  - Top-selling items & categories
  - Sales by payment method (cash, UPI, cards)
  - Inventory & wastage reports

### 3. Shop Management / POS (In-Store)
- Fast **bill generation** for walk-in customers
- View / reprint previous bills
- Real-time inventory updates on sale
- Record wastage / damage
- Worker attendance (optional check-in/out)
- End-of-day summary (cash, UPI, cards breakup)
- **Offline-first PWA**:
  - Works if internet is down
  - Stores bills locally
  - Syncs with server when connection returns
- Intended to run **only on shop Wi-Fi / local network**

---

## 🏗️ High-Level Architecture

```mermaid
flowchart LR
    subgraph Client Apps
        A[Customer Web<br/>React SPA]
        B[Admin Portal<br/>React SPA]
        C[Shop POS<br/>React PWA]
    end

    A --> G[GraphQL BFF]
    B --> G
    C --> G

    subgraph Backend Microservices (Spring Boot)
        U[User & Auth Service]
        P[Product & Inventory Service]
        O[Order & Billing Service]
        N[Notification / Marketing Service]
        L[Loyalty & Coupons Service]
    end

    G --> U
    G --> P
    G --> O
    G --> N
    G --> L

    subgraph Data Layer
        DB1[(PostgreSQL / MySQL)]
        DB2[(Redis)]
    end

    U --> DB1
    P --> DB1
    O --> DB1
    N --> DB1
    L --> DB1

    G --> DB2
    O --> DB2
