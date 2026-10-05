# 🗺️ Technical Roadmap

> Priorities: **P0** essential · **P1** high value · **P2** important · **P3** optional · **P4** low return at this stage

This roadmap is organized by **phase, not by calendar deadline**. One year is the baseline target — not a hard constraint per phase. If a phase takes longer, that's fine; the plan continues. Progress is tracked by capability (see ([`PROGRESS.md`](./PROGRESS.md))), not by whether a date was hit.


---

<!-- ## Phase 0 — Bridge

**Goal:** move past absolute zero without committing to a final language/stack yet.

- [ ] **P0** — Object-Oriented Programming (classes, inheritance, encapsulation, polymorphism)
- [ ] **P0** — Git and GitHub (flow, branches, commits, PRs)
- [ ] **P1** — SQL with PostgreSQL (queries, joins, aggregations, subqueries, transactions, procedures)
- [ ] **P1** — REST API concepts, HTTP, middleware (via Node/Express — concepts transfer to Spring Boot)
- [ ] **P2** — HTML fundamentals (minimum web vocabulary)
- [ ] **P1** — GitHub Foundations certification
- [ ] **P4** — Advanced CSS, Bootstrap, Tailwind, SASS, React, React Native *(out of scope — deliberately skipped)* -->

## Phase 1 — Algorithms and Programming Logic

- [ ] **P0** — Programming logic, conditionals/loops, functions, recursion
- [ ] **P0** — Variables and data types
- [ ] **P0** — Control flow: loops and conditionals
- [ ] **P0** — Arrays and matrices
- [ ] **P0** — Data structures (lists, stacks, queues, trees, hash maps) and Big O complexity *(added — the single most tested area in real technical interviews)*
- [ ] **P0** — Git / GitHub (flow, branches, commits, PRs)

---

## Phase 2 — Object-Oriented Programming (OOP)

**Goal:** master the concepts that structure the backend.

- [ ] **P1** — UML
- [ ] **P0** — Abstraction, Encapsulation, Inheritance, and Polymorphism
- [ ] **P0** — Java Collections (List, Set, Map)
- [ ] **P1** — Enums
- [ ] **P1** — Generics
- [ ] **P0** — Exception handling
- [ ] **P2** — Java I/O
- [ ] **P1** — Practical projects

---

## Phase 3 — Frameworks and APIs

**Spring Boot:**

- [ ] **P1** — Maven
- [ ] **P0** — Dependency Injection
- [ ] **P0** — Inversion of Control
- [ ] **P1** — Spring Beans
- [ ] **P0** — Building REST APIs with Spring
- [ ] **P0** — Controllers, Services, and Repositories
- [ ] **P1** — Pagination, Sorting, and complex Filters
- [ ] **P2** — Filters, Interceptors, and DispatcherServlet
- [ ] **P1** — Exception handling (RFC 7807)
- [ ] **P2** — API integration with OpenFeign

---

## Phase 4 — Database Integration

- [ ] **P0** — Spring Data JPA (Entities, Jakarta Persistence, etc.)
- [ ] **P0** — Relationships: One-to-One, One-to-Many, Many-to-Many, etc.
- [ ] **P0** — PostgreSQL *(primary — matches the target job market directly)*
- [ ] **P3** — MySQL *(optional — same relational concepts as PostgreSQL; skip or skim)*
- [ ] **P3** — MongoDB *(optional — different paradigm, worth a conceptual pass, not deep practice right now)*
- [ ] **P2** — File integration (OpenCSV)
- [ ] **P1** — Practical portfolio projects

---

## Phase 5 — Quality and Testing

- [ ] **P0** — Test pyramid strategy
- [ ] **P0** — Unit testing with JUnit
- [ ] **P0** — Test Doubles and Mocks with Mockito
- [ ] **P2** — Mutation testing with Pitest
- [ ] **P1** — Integration testing with Testcontainers (AWS, WireMock, etc.)
- [ ] **P2** — End-to-end (E2E) testing with BDD, Cucumber, and Gherkin

---

## Phase 6 — Differentiators

- [ ] **P1** — Portfolio practical projects
- [ ] **P1** — Architecture mindset
- [ ] **P1** — Observability
- [ ] **P1** — Software security

---

## Phase 7 — Job Application Prep

**Goal:** be ready and visible to the market.

- [ ] **P0** — Finished portfolio (2–3 solid projects, with README, tests, documented decisions)
- [ ] **P0** — Resume and LinkedIn aligned with the target role
- [ ] **P1** — Technical interview practice (DSA + systems concepts)
- [ ] **P1** — Active applications at target companies (fintech, data infrastructure)

---

## Open decisions (deliberately deferred)

- Final segment: Fintech/Payments vs. Infrastructure/Data Streaming — to be decided later, with more hands-on experiencewq


## 🏗️ Portfolio Plan: Three Connected Projects

My portfolio is **one system that grows in three stages**, not three unrelated projects. Each stage goes deeper into the same problem: moving money correctly in a system that cannot afford to fail.

> I will only call a project "done" when it has passing tests in CI, a README with run instructions and technical decisions, and I can explain every decision without looking anything up.

---

### 🥇 Project 1 — Payments API with a Ledger (Anchor Project)

**Stack:** Java · Spring Boot · PostgreSQL · Testcontainers

**What it is:** a mini payment processor. A merchant creates a charge, which can be authorized, captured, and refunded.

**What it must include:**

- [ ] **Idempotency keys:** sending the same request twice creates only one charge
- [ ] **Double-entry ledger:** every movement creates debit and credit entries that always sum to zero
- [ ] **State machine:** valid charge transitions are allowed, invalid ones are blocked
- [ ] **Concurrency control:** optimistic or pessimistic locking, so two simultaneous withdrawals cannot overdraw a balance
- [ ] **Transactional outbox:** an event is published only if the transaction committed
- [ ] **Webhooks** with retry and exponential backoff
- [ ] **Integration tests with Testcontainers**, including a concurrency test (for example: 100 threads, same key, exactly one charge)
- [ ] **Audit log** and safe handling of sensitive data (no real card numbers, only simulated tokens)
- [ ] **README and ADRs** (Architecture Decision Records): why optimistic locking, why double-entry, and so on

**Why it matters:** it lets me answer common payments interview questions with my own code:

- *How do you prevent duplicate charges?*
- *What happens if the service crashes in the middle of a transaction?*

---

### 🥈 Project 2 — Event Pipeline with Kafka

**What it is:** an extension of Project 1. Payment events flow through Kafka, and consumers calculate balances, flag simple suspicious patterns, and generate reports.

**What it must include:**

- [ ] Idempotent consumers
- [ ] Retries and a dead-letter queue
- [ ] Ordering guaranteed by message key
- [ ] Basic metrics (Prometheus and Grafana)
- [ ] A written explanation of the **at-least-once vs exactly-once** trade-off

**Why it matters:** it connects Fintech and Data Infrastructure, so I keep both paths open until I have enough hands-on experience to choose.

---

### 🥉 Project 3 — Failure and Load Lab (The Differentiator)

**What it is:** a reproducible report showing how the system behaves under stress.

**Scenarios to test:**

- [ ] Load testing with k6
- [ ] Duplicate messages
- [ ] Database failure in the middle of a transaction
- [ ] Consumer restart

**What it must include:** the scenarios, the results, what broke, what I fixed, and a postmortem-style analysis.

**Why it matters:** it shows that I think about reliability, not only about making things work. This is exactly what high-criticality systems require.

---

## 🧭 Order of Execution (by phase, not by date)

1. **Fundamentals + Spring/SQL:** exercises with tests. These are practice, not portfolio yet.
2. **Project 1:** once I am comfortable with Spring Boot, SQL, and testing.
3. **Project 2:** once Project 1 is stable.
4. **Project 3:** at the end, built on top of what already exists.
5. **Job applications:** start once Project 1 is solid. Do not wait for Project 3.

---

## 🔭 Later (not now)

- Redis, AWS, and deeper observability, only when a project needs them
- One small open source contribution (documentation fix or a well-written issue)
- Choosing between **Fintech/Payments** and **Data Infrastructure/Streaming**, after real hands-on experience

---

## 🚫 What I Will Not Build

Shopping cart e-commerce, CRUD-only banking apps, library systems, to-do apps. They do not demonstrate correctness, reliability, or scale.