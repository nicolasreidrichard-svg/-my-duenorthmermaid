# 🧜 My DueNorth Mermaid

> **Making Mermaid AWESOME** — A comprehensive showcase of [Mermaid](https://mermaid.js.org/) diagram types, from simple flowcharts to complex entity-relationship diagrams.

[![Mermaid](https://img.shields.io/badge/Made%20with-Mermaid-ff69b4.svg)](https://mermaid.js.org/)
[![Diagrams](https://img.shields.io/badge/Diagrams-11%20Types-blue.svg)](#diagram-types)

---

## Table of Contents

- [Flowchart](#-flowchart)
- [Sequence Diagram](#-sequence-diagram)
- [Gantt Chart](#-gantt-chart)
- [Class Diagram](#-class-diagram)
- [State Diagram](#-state-diagram)
- [Entity Relationship Diagram](#-entity-relationship-diagram)
- [User Journey](#-user-journey)
- [Pie Chart](#-pie-chart)
- [Quadrant Chart](#-quadrant-chart)
- [Timeline](#-timeline)
- [Mindmap](#-mindmap)

---

## 🔷 Flowchart

A flowchart showing a typical software development workflow:

```mermaid
flowchart TD
    A([🚀 Start]) --> B{New Feature?}
    B -- Yes --> C[Create Feature Branch]
    B -- No --> D[Create Bugfix Branch]
    C --> E[Write Code]
    D --> E
    E --> F[Write Tests]
    F --> G{Tests Pass?}
    G -- No --> E
    G -- Yes --> H[Open Pull Request]
    H --> I{Code Review}
    I -- Changes Requested --> E
    I -- Approved --> J[Merge to Main]
    J --> K[Deploy to Staging]
    K --> L{QA Approved?}
    L -- No --> E
    L -- Yes --> M([🎉 Deploy to Production])

    style A fill:#4CAF50,color:#fff
    style M fill:#4CAF50,color:#fff
    style G fill:#FF9800,color:#fff
    style I fill:#FF9800,color:#fff
    style L fill:#FF9800,color:#fff
```

---

## 🔁 Sequence Diagram

A sequence diagram illustrating a user authentication flow:

```mermaid
sequenceDiagram
    actor User
    participant Browser
    participant API as REST API
    participant Auth as Auth Service
    participant DB as Database

    User->>Browser: Enter credentials
    Browser->>API: POST /auth/login
    API->>Auth: Validate credentials
    Auth->>DB: Query user record
    DB-->>Auth: Return user data
    Auth-->>API: JWT token
    API-->>Browser: 200 OK + token
    Browser-->>User: Redirect to dashboard

    Note over User,Browser: Session begins

    User->>Browser: Request protected resource
    Browser->>API: GET /resource (Bearer token)
    API->>Auth: Verify token
    Auth-->>API: Token valid ✓
    API->>DB: Fetch resource
    DB-->>API: Resource data
    API-->>Browser: 200 OK + data
    Browser-->>User: Display resource
```

---

## 📅 Gantt Chart

A project timeline for building a web application:

```mermaid
gantt
    title Web Application Project Timeline
    dateFormat  YYYY-MM-DD
    excludes weekends

    section Planning
    Requirements gathering     :done,    req,  2024-01-01, 2024-01-10
    Architecture design        :done,    arch, 2024-01-08, 2024-01-18
    Tech stack selection       :done,    tech, 2024-01-15, 2024-01-19

    section Development
    Backend API                :active,  api,  2024-01-22, 30d
    Database schema            :done,    db,   2024-01-22, 10d
    Frontend components        :         fe,   2024-01-29, 25d
    Authentication module      :         auth, 2024-02-05, 10d
    Integration                :         int,  after fe,   7d

    section Testing
    Unit tests                 :         ut,   after api,  10d
    Integration tests          :         it,   after int,  7d
    Performance testing        :         pt,   after it,   5d
    User acceptance testing    :         uat,  after pt,   7d

    section Deployment
    Staging deployment         :         stg,  after uat,  3d
    Production deployment      :         prod, after stg,  2d
    Post-launch monitoring     :         mon,  after prod, 14d
```

---

## 🏛️ Class Diagram

A class diagram for an e-commerce domain model:

```mermaid
classDiagram
    class User {
        +int id
        +string name
        +string email
        +string passwordHash
        +Date createdAt
        +login(email, password) bool
        +updateProfile(data) void
        +getOrders() Order[]
    }

    class Product {
        +int id
        +string name
        +string description
        +float price
        +int stockQty
        +string category
        +isAvailable() bool
        +updateStock(qty) void
    }

    class Order {
        +int id
        +Date createdAt
        +string status
        +float totalAmount
        +addItem(product, qty) void
        +removeItem(productId) void
        +calculateTotal() float
        +submit() void
    }

    class OrderItem {
        +int id
        +int quantity
        +float unitPrice
        +getSubtotal() float
    }

    class Cart {
        +int id
        +addProduct(product) void
        +removeProduct(productId) void
        +checkout() Order
        +clear() void
    }

    class Payment {
        +int id
        +float amount
        +string method
        +string status
        +Date processedAt
        +process() bool
        +refund() bool
    }

    User "1" --> "1" Cart : has
    User "1" --> "0..*" Order : places
    Order "1" *-- "1..*" OrderItem : contains
    OrderItem "0..*" --> "1" Product : references
    Order "1" --> "1" Payment : paid via
```

---

## 🔄 State Diagram

A state diagram for an order lifecycle:

```mermaid
stateDiagram-v2
    [*] --> Pending : Order Placed

    Pending --> Processing : Payment Confirmed
    Pending --> Cancelled : Customer Cancels

    Processing --> Packed : Items Picked & Packed
    Processing --> Cancelled : Out of Stock

    Packed --> Shipped : Handed to Carrier
    Packed --> Processing : Packaging Error

    Shipped --> OutForDelivery : In Local Area
    Shipped --> Delayed : Weather/Logistics Issue

    Delayed --> OutForDelivery : Issue Resolved

    OutForDelivery --> Delivered : Customer Receives
    OutForDelivery --> FailedDelivery : No One Home

    FailedDelivery --> OutForDelivery : Re-attempt
    FailedDelivery --> Returned : Max Attempts Reached

    Delivered --> Refunded : Return Requested
    Returned --> Refunded : Return Processed

    Cancelled --> [*]
    Delivered --> [*]
    Refunded --> [*]

    note right of Shipped
        Tracking number
        emailed to customer
    end note
```

---

## 🗄️ Entity Relationship Diagram

An ER diagram for a blog platform database:

```mermaid
erDiagram
    USER {
        int id PK
        string username UK
        string email UK
        string password_hash
        string avatar_url
        string bio
        datetime created_at
        datetime updated_at
    }

    POST {
        int id PK
        int author_id FK
        int category_id FK
        string title
        string slug UK
        text content
        string status
        datetime published_at
        datetime created_at
        datetime updated_at
    }

    CATEGORY {
        int id PK
        string name UK
        string slug UK
        string description
    }

    TAG {
        int id PK
        string name UK
        string slug UK
    }

    POST_TAG {
        int post_id FK
        int tag_id FK
    }

    COMMENT {
        int id PK
        int post_id FK
        int author_id FK
        int parent_id FK
        text content
        datetime created_at
    }

    LIKE {
        int id PK
        int user_id FK
        int post_id FK
        datetime created_at
    }

    USER ||--o{ POST : "authors"
    USER ||--o{ COMMENT : "writes"
    USER ||--o{ LIKE : "gives"
    POST }o--|| CATEGORY : "belongs to"
    POST ||--o{ POST_TAG : "tagged with"
    TAG ||--o{ POST_TAG : "applied to"
    POST ||--o{ COMMENT : "receives"
    COMMENT }o--o{ COMMENT : "replies to"
    POST ||--o{ LIKE : "receives"
```

---

## 🧭 User Journey

A user journey map for onboarding a new customer:

```mermaid
journey
    title New Customer Onboarding Journey
    section Discovery
      Find website via search: 3: User
      Browse landing page: 4: User
      Read testimonials: 4: User
    section Sign Up
      Click "Get Started": 5: User
      Fill registration form: 2: User
      Verify email: 3: User
      Complete profile: 3: User, Support
    section First Use
      Watch tutorial video: 4: User
      Create first project: 5: User
      Invite team members: 4: User, Support
    section Engagement
      Use core features: 5: User
      Explore integrations: 4: User
      Contact support: 3: User, Support
    section Retention
      Upgrade to paid plan: 5: User
      Refer a friend: 5: User
```

---

## 🥧 Pie Chart

Distribution of programming languages used in the project:

```mermaid
pie title Programming Languages Used
    "TypeScript" : 42
    "JavaScript" : 28
    "Python" : 15
    "Go" : 8
    "Shell" : 5
    "Other" : 2
```

---

## 📊 Quadrant Chart

Feature prioritization matrix:

```mermaid
quadrantChart
    title Feature Prioritization Matrix
    x-axis Low Effort --> High Effort
    y-axis Low Impact --> High Impact
    quadrant-1 Do First
    quadrant-2 Plan
    quadrant-3 Low Priority
    quadrant-4 Delegate

    Dark Mode: [0.2, 0.85]
    API Rate Limiting: [0.35, 0.9]
    OAuth Integration: [0.55, 0.88]
    Bulk Export: [0.3, 0.6]
    AI Suggestions: [0.75, 0.95]
    Emoji Reactions: [0.15, 0.3]
    Advanced Filters: [0.45, 0.7]
    Real-time Collaboration: [0.8, 0.85]
    Audit Logs: [0.4, 0.5]
    Mobile App: [0.85, 0.75]
    Keyboard Shortcuts: [0.2, 0.55]
    Multi-language Support: [0.65, 0.6]
```

---

## 📆 Timeline

Key milestones in Mermaid's history:

```mermaid
timeline
    title History of Mermaid.js
    2014 : Knut Sveidqvist starts the project
    2016 : v0.5 - First public release
         : Flowcharts and sequence diagrams
    2017 : v7.0 - Major stability improvements
         : Gantt chart support added
    2019 : v8.0 - Complete rewrite
         : Class diagrams introduced
    2020 : v8.5 - State diagrams
         : ER diagrams added
    2021 : v8.9 - Pie charts & User journeys
         : GitHub native rendering support
    2022 : v9.0 - Complete TypeScript rewrite
         : Quadrant charts & Mindmaps
    2023 : v10.0 - Architecture overhaul
         : Block diagrams & XY charts
    2024 : v11.0 - New themes and renderers
         : Enhanced accessibility features
```

---

## 🧠 Mindmap

A mindmap showing the ecosystem around Mermaid.js:

```mermaid
mindmap
  root((Mermaid.js))
    Diagram Types
      Flowchart
      Sequence
      Gantt
      Class
      State
      ER
      Journey
      Pie
      Quadrant
      Timeline
      Mindmap
    Integrations
      GitHub
        Native rendering
        Actions workflows
      VS Code
        Extensions
        Preview
      Confluence
      Notion
      Obsidian
    Rendering
      Browser
        CDN
        npm package
      CLI
        mmdc
        SVG output
        PNG output
      Server-side
    Themes
      Default
      Forest
      Dark
      Neutral
      Base
```

---

## 🚀 Getting Started with Mermaid

### In GitHub Markdown

Simply wrap your diagram in a fenced code block with `mermaid` as the language:

````markdown
```mermaid
flowchart LR
    A[Start] --> B[End]
```
````

### With the Mermaid CLI

```bash
# Run without installing (recommended)
npx @mermaid-js/mermaid-cli mmdc -i diagram.mmd -o diagram.svg

# Or install globally
npm install -g @mermaid-js/mermaid-cli@11.4.1

# Render a diagram
mmdc -i diagram.mmd -o diagram.svg
```

### In a Web Page

```html
<!DOCTYPE html>
<html>
  <body>
    <pre class="mermaid">
      flowchart LR
          A[Start] --> B[End]
    </pre>
    <script type="module">
      // Pin to a specific version to prevent supply chain attacks
      import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11.4.1/dist/mermaid.esm.min.mjs';
      mermaid.initialize({ startOnLoad: true, theme: 'default' });
    </script>
  </body>
</html>
```

---

## 📚 Resources

| Resource | Link |
|----------|------|
| 📖 Official Docs | [mermaid.js.org](https://mermaid.js.org/) |
| 🎮 Live Editor | [mermaid.live](https://mermaid.live/) |
| 💬 Community | [GitHub Discussions](https://github.com/mermaid-js/mermaid/discussions) |
| 🐛 Issues | [GitHub Issues](https://github.com/mermaid-js/mermaid/issues) |
| 📦 npm Package | [npmjs.com/package/mermaid](https://www.npmjs.com/package/mermaid) |

---

<div align="center">
  Made with ❤️ and <strong>Mermaid</strong> 🧜
</div>
