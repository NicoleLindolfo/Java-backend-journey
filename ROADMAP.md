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


Projeto âncora: API de pagamentos/carteira em Spring Boot + PostgreSQL, com idempotency keys, lançamentos em partida dobrada (ledger), controle de concorrência, testes de integração e README com decisões técnicas documentadas. Ele vira Tier 3, com chance de Tier 4.
README em inglês simples desde o início.
Kafka, Redis, AWS, observabilidade.
Primeira contribuição open source pequena (documentação ou issue bem escrita).
Escolher entre Fintech e Data Infra, depois de ter experiência prática.

-Projeto 1 (flagship): API de pagamentos com ledger

O que é: um mini processador de pagamentos em Java + Spring Boot + PostgreSQL. Um comerciante cria uma cobrança, ela é autorizada, capturada e pode ser reembolsada.

O que ele precisa ter (é isso que o torna Tier 3 e não "projeto de estudante"):

Chave de idempotência: a mesma requisição enviada duas vezes cria uma cobrança só.
Ledger em partida dobrada: cada movimentação gera lançamentos de débito e crédito que sempre fecham em zero.
Máquina de estados da cobrança, com transições válidas e inválidas bloqueadas.
Controle de concorrência: lock otimista ou pessimista, para dois saques simultâneos não estourarem o saldo.
Transactional outbox: o evento só é publicado se a transação confirmou.
Webhooks com retry e backoff.
Testes de integração com Testcontainers, incluindo um teste de concorrência (ex.: 100 threads, mesma chave, uma cobrança).
Log de auditoria e cuidado com dados sensíveis (não guardar número de cartão, usar token simulado).
README e ADRs (decisões arquiteturais): por que escolhi lock otimista, por que partida dobrada.

Como te ajuda: cobre quase toda pergunta típica de entrevista de pagamentos ("como evitar cobrança duplicada?", "o que acontece se o serviço cair no meio da transação?") com código seu para apontar.



Projeto 2: pipeline de eventos com Kafka

O que é: uma extensão do Projeto 1. Os eventos de pagamento passam por Kafka, e consumidores calculam saldos, detectam padrões suspeitos simples e geram relatórios.

Precisa ter: consumidor idempotente, retries, dead-letter queue, ordenação por chave, métricas básicas (Prometheus/Grafana) e a explicação do trade-off at-least-once vs exactly-once.

Como te ajuda: é a ponte entre Fintech e Infra de Dados, então você mantém as duas portas abertas sem decidir agora. Também mostra que você pensa em sistemas distribuídos, não só em um serviço isolado.



Projeto 3: laboratório de falhas e carga (o diferenciador)

O que é: um relatório reproduzível provando que o sistema se comporta bem sob estresse: teste de carga (k6), duplicação de mensagens, queda do banco no meio de uma transação, reinício de consumidor.

Precisa ter: cenários, resultados, o que quebrou, o que você corrigiu e uma análise no formato de postmortem.

Como te ajuda: quase nenhum júnior faz isso. É a evidência de que você pensa em confiabilidade, justamente o que sua área-alvo exige, e vira ótimo material de conversa na entrevista. Este é o seu Tier 4.

Ordem sugerida (por fase, não por data, como você já faz)
Fundamentos + Spring/SQL: exercícios com testes. Ainda não são portfólio.
Projeto 1 quando você dominar Spring Boot, SQL e testes (provavelmente a maior parte do meio do ano).
Projeto 2 com o Projeto 1 estável.
Projeto 3 no final, sobre o que já existe.
Candidaturas só depois do Projeto 1 estar sólido. Não espere o 3 terminar para começar a se candidatar.