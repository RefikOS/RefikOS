# RefikOS

<img width="1254" height="1254" alt="image" src="https://github.com/user-attachments/assets/e8e0bc79-25be-4a12-92a8-c989304c46ca" />

**RefikOS is a modular operating system for humanitarian organizations.**

RefikOS helps NGOs, foundations, aid organizations and disaster-response teams manage donations, volunteers, field operations, logistics, warehouses, campaigns, finance workflows and rescue coordination from a single extensible platform.

> **STK’ların dijital refiki.**  
> **One platform for every humanitarian mission.**

---

## Vision

Humanitarian organizations usually work with fragmented tools: one system for donations, another for volunteers, spreadsheets for warehouses, messaging apps for field teams and manual processes for approvals.

RefikOS aims to become the digital backbone of these organizations by bringing all critical workflows into a modular, secure and extensible platform.

RefikOS is not only a donation platform. It is designed as a complete NGO ERP and field operation system.

---

## What RefikOS Solves

RefikOS is designed to support organizations that need to manage:

- Donations and campaigns
- Members and volunteers
- Projects and funds
- Aid distribution
- Warehouses and inventory
- Logistics and shipment tracking
- Disaster and rescue operations
- Field teams and mobile workflows
- Finance, audit and approval processes
- Scholarships and education programs
- Qurban and seasonal aid operations
- Multi-branch and multi-organization structures

---

## Core Principles

- **Modular by design**  
  Every organization can enable only the modules it needs.

- **Multi-tenant ready**  
  Multiple NGOs can run on the same platform with strong organization-level separation.

- **Cloud and on-premise friendly**  
  RefikOS can be delivered as SaaS, private cloud or self-hosted on-premise.

- **Audit-first architecture**  
  Financial and operational actions must be traceable.

- **Offline-first field operations**  
  Disaster and field modules should work even when internet access is unstable.

- **API-first development**  
  Every module should be designed for integration with external systems.

- **Test-driven quality**  
  Business-critical flows must be covered with unit, integration and E2E tests.

---

## Product Positioning

**RefikOS is a modular NGO ERP + disaster and field operations platform.**

It can be presented as:

> RefikOS gives humanitarian organizations a single digital backbone for donations, volunteers, logistics, field operations and financial governance.

Or in Turkish:

> RefikOS, yardım kuruluşlarının bağıştan gönüllü yönetimine, sahadan depoya, lojistikten finansal onaya kadar tüm operasyonlarını modüler şekilde yöneten dijital platformdur.

---

## Sub-Brands / Modules

RefikOS is built around a core platform and optional product modules.

```txt
RefikOS Core          → Platform foundation
RefikOS Donations     → Donation and campaign management
RefikOS Volunteers    → Volunteer coordination
RefikOS Rescue        → Disaster and rescue operations
RefikOS Field         → Mobile field operations
RefikOS Warehouse     → Inventory and aid storage
RefikOS Logistics     → Shipment and distribution
RefikOS Finance       → Accounting, audit and reporting
RefikOS Education     → Scholarship and student programs
RefikOS Qurban        → Qurban organization workflows
```

---

## High-Level Architecture

RefikOS is designed as a **modular monolith core** supported by selected satellite services.

The goal is not to create hundreds of microservices from day one. Instead, the core business capabilities live inside a well-structured modular monolith. Only services with different scaling, security or operational needs are separated.

```txt
                         ┌───────────────────────────────┐
                         │           RefikOS Web          │
                         │      React + TypeScript        │
                         └───────────────┬───────────────┘
                                         │
                                         ▼
┌──────────────────────────────────────────────────────────────────┐
│                         RefikOS Core API                         │
│                                                                  │
│  Identity  │ Tenant │ RBAC │ Audit │ Workflow │ Module Registry │
│                                                                  │
│  Donations │ Volunteers │ Funds │ Projects │ Finance │ Documents │
│                                                                  │
│  Warehouse │ Logistics │ Education │ Qurban │ Aid Distribution   │
└───────────────────────────────┬──────────────────────────────────┘
                                │
                 ┌──────────────┼──────────────┐
                 ▼              ▼              ▼
        ┌──────────────┐ ┌──────────────┐ ┌────────────────┐
        │ Notification │ │ Payment/POS  │ │ Field / Rescue │
        │ Service      │ │ Service      │ │ Service        │
        └──────────────┘ └──────────────┘ └────────────────┘
```

---

## Why Modular Monolith First?

RefikOS may eventually contain many modules. However, many modules should not automatically mean many microservices.

A premature microservice architecture can create unnecessary operational complexity:

- Distributed transactions
- Hard debugging
- More DevOps burden
- Complex deployments
- Eventual consistency problems in financial flows
- Difficult local development

For this reason, RefikOS starts with a modular monolith and separates only the services that truly need isolation.

---

## Suggested Satellite Services

### Notification Service

Responsible for:

- Email
- SMS
- Push notifications
- Retry mechanisms
- Notification templates
- Delivery logs

This service is separated because notification traffic can become heavy and should not block the core platform.

### Payment Service

Responsible for:

- Payment provider integrations
- Virtual POS integrations
- Payment callbacks
- Refund flows
- Secure payment boundaries

This service is separated because payment operations have special security, compliance and operational needs.

### Field / Rescue Service

Responsible for:

- Offline-first field data
- Disaster operation records
- Mobile sync
- GPS-based field tasks
- Rescue team coordination

This service is separated because field and disaster operations have very different availability and synchronization requirements.

---

## Database Strategy

RefikOS avoids database-per-module complexity in the beginning.

Recommended model:

```txt
Core Platform       → PostgreSQL
Notification Svc    → Own database
Payment Svc         → Own database
Field/Rescue Svc    → Own database or sync database
```

Inside the core platform, modules can be separated logically with schemas:

```txt
identity.*
tenant.*
donations.*
volunteers.*
finance.*
warehouse.*
logistics.*
workflow.*
audit.*
```

This provides isolation while keeping cross-module transactions possible.

---

## Multi-Tenant Strategy

RefikOS should support multiple deployment models.

### Shared Cloud Model

Suitable for small and mid-sized NGOs.

```txt
Single RefikOS Cloud
├── NGO A
├── NGO B
└── NGO C
```

Each organization is separated by tenant configuration and authorization boundaries.

### Dedicated Cloud Model

Suitable for large NGOs or foundations.

```txt
Dedicated RefikOS Instance
└── One large organization
```

### On-Premise Model

Suitable for institutions that need full control over data and infrastructure.

```txt
Customer Infrastructure
└── Self-hosted RefikOS
```

---

## Product Editions

RefikOS can be packaged as different editions.

### RefikOS Community

For small NGOs and open-source users.

Includes:

- Basic organization management
- Members
- Volunteers
- Donations
- Campaigns
- Basic reports

### RefikOS Cloud

Managed SaaS platform.

Includes:

- Hosted RefikOS instance
- Automatic updates
- Backups
- Standard integrations
- User support

### RefikOS Enterprise

For large foundations and institutions.

Includes:

- Advanced workflows
- Advanced reporting
- Finance and audit controls
- Custom integrations
- Dedicated infrastructure options

### RefikOS Field

For field and disaster operations.

Includes:

- Offline-first mobile workflows
- Rescue team coordination
- Field task management
- GPS-based operations
- Local sync support

### RefikOS On-Premise

For organizations that require full data control.

Includes:

- Self-hosted deployment
- Private infrastructure
- Custom security policies
- Internal network support

---

## Technology Stack

### Backend

- Go
- REST / OpenAPI
- PostgreSQL
- sqlc + pgx
- Goose or golang-migrate
- RabbitMQ or PostgreSQL-based event bus
- Docker

### Frontend

- React
- TypeScript
- Vite
- TanStack Query
- OpenAPI client generation
- Modular route registry
- Permission-based UI rendering

### Testing

- Go unit tests
- Integration tests with test containers
- API contract tests
- Frontend component tests
- E2E tests with Playwright

---

## Repository Structure

```txt
refikos/
├── cmd/
│   ├── core-api/
│   ├── notification-svc/
│   ├── payment-svc/
│   └── field-svc/
│
├── internal/
│   ├── platform/
│   │   ├── auth/
│   │   ├── tenant/
│   │   ├── rbac/
│   │   ├── audit/
│   │   ├── workflow/
│   │   ├── eventbus/
│   │   ├── module/
│   │   └── money/
│   │
│   └── modules/
│       ├── donations/
│       ├── volunteers/
│       ├── rescue/
│       ├── warehouse/
│       ├── logistics/
│       ├── finance/
│       ├── education/
│       └── qurban/
│
├── web/
│   └── src/
│       ├── app/
│       ├── platform/
│       └── modules/
│
├── migrations/
├── docs/
├── deployments/
├── tests/
└── README.md
```

---

## Go Module Interface Example

Each RefikOS module should register itself into the platform.

```go
type Module interface {
    Name() string
    RegisterRoutes(router Router)
    Permissions() []Permission
    Subscribe(bus EventBus)
    Migrate(db DB) error
}
```

This allows modules to be enabled, disabled and discovered by the core platform.

---

## Frontend Modularity

The frontend should also be modular.

Each module can define:

- Routes
- Sidebar menu items
- Dashboard cards
- Permissions
- API hooks
- Components

Example:

```txt
web/src/modules/donations/
├── routes.tsx
├── menu.ts
├── dashboard.tsx
├── permissions.ts
├── api.ts
└── components/
```

When a module is enabled, the frontend can automatically add its menu items, routes and dashboard cards based on module metadata.

---

## Module Metadata Example

```ts
export const donationsModule = {
  name: 'donations',
  title: 'Donations',
  menu: [
    {
      label: 'Donations',
      path: '/donations',
      permission: 'donations.read'
    }
  ],
  dashboardCards: [
    {
      key: 'total-donations',
      permission: 'donations.read'
    }
  ]
}
```

---

## Security Principles

- Tenant isolation must be enforced in middleware and repositories.
- Every request must include user, tenant and permission context.
- Sensitive operations must be audited.
- Financial actions must be immutable or versioned.
- Payment data must be isolated from general business data.
- Access control should be permission-based, not only role-based.

---

## Development Standards

Every module should include:

- Unit tests
- Integration tests
- Database migrations
- API documentation
- Permission definitions
- Audit event definitions
- E2E scenarios for critical flows

Business-critical flows should not be merged without test coverage.

---

## Example Critical E2E Flows

```txt
Donation Flow
1. Create donor
2. Create campaign
3. Create donation
4. Process payment callback
5. Assign donation to fund
6. Generate receipt
7. Create audit record

Volunteer Flow
1. Register volunteer
2. Approve volunteer
3. Assign to field task
4. Track task completion
5. Generate activity report

Warehouse Flow
1. Add inventory item
2. Receive stock
3. Reserve stock for aid package
4. Dispatch package
5. Confirm delivery
6. Update inventory ledger

Rescue Flow
1. Create disaster incident
2. Create field team
3. Assign rescue task
4. Sync mobile field data
5. Close task with report
```

---

## Documentation Plan

The project should be documented in separate files under `/docs`.

```txt
docs/
├── 00-product-vision.md
├── 01-architecture-overview.md
├── 02-core-platform.md
├── 03-module-system.md
├── 04-multi-tenancy.md
├── 05-database-strategy.md
├── 06-frontend-architecture.md
├── 07-field-offline-architecture.md
├── 08-security-and-rbac.md
├── 09-testing-strategy.md
├── 10-deployment-models.md
└── 11-roadmap.md
```

---

## Roadmap

### Phase 1 — Foundation

- Core API skeleton
- Authentication
- Tenant management
- RBAC
- Audit log
- Module registry
- PostgreSQL migrations
- React admin shell

### Phase 2 — First Business Modules

- Donations
- Campaigns
- Members
- Volunteers
- Basic finance
- Documents

### Phase 3 — Operations

- Warehouse
- Logistics
- Aid distribution
- Approval workflows
- Advanced reporting

### Phase 4 — Field and Disaster

- Field service
- Mobile sync
- Offline-first workflows
- Rescue coordination
- GPS-based tasks

### Phase 5 — Enterprise

- On-premise deployment
- Advanced audit
- Custom integrations
- Data export/import
- Multi-branch organization support

---

## Naming and Brand System

Primary brand:

```txt
RefikOS
```

Suggested tagline:

```txt
Tek Platform. Tüm İyilik Hareketleri.
```

English tagline:

```txt
One Platform. Every Humanitarian Mission.
```

Sub-brand examples:

```txt
RefikOS Core
RefikOS Donations
RefikOS Rescue
RefikOS Field
RefikOS Volunteers
RefikOS Finance
RefikOS Warehouse
RefikOS Logistics
RefikOS Education
RefikOS Qurban
```

---

## License

To be decided.

Possible options:

- AGPL-3.0 for strong open-source protection
- Apache-2.0 for ecosystem adoption
- Open-core model with commercial enterprise modules

---

## Status

RefikOS is currently in the architecture and foundation planning phase.

The first goal is to build a clean, tested and extensible foundation before implementing many business modules.

---

## Contribution

Contribution guidelines will be added after the initial architecture and repository structure are completed.

