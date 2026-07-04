# Khushi Talaviya

Email: khushitalaviya0912@gmail.com | LinkedIn: linkedin.com/in/khushitalaviya | GitHub: github.com/talaviyakhushi | Portfolio: khushitalaviya.vercel.app | Location: New York, NY

## Summary

Software engineer with hands-on Python backend and ML-model-integration experience (OpenAI vision/embedding models in production), plus a distributed-systems research background and CI/CD-driven deployment experience on AWS. Comfortable working across backend services, REST APIs, and cloud infrastructure; looking to grow into ML infrastructure and platform engineering.

## Work Experience

### Software Developer Co-op — Forty7 (2026)

- Deployed a production ML inference service end-to-end by building an AI pricing tool (Spring Boot + Java 21 + gpt-4o vision) with a GitHub Actions CI/CD pipeline that builds the JDK 21 artifact, ships it to EC2, and restarts the service via systemd — sole owner of the deployment path.
- Enabled reliable model inference at the API boundary by gating both estimation endpoints with reCAPTCHA server-side verification before any OpenAI call, and by adding a pre-inference completeness check that skips the model call (and its cost) when input data is insufficient.
- Validated model output quality by benchmarking price estimates from the vision-classification pipeline against 3,000+ real marketplace listings, reaching 90% accuracy.
- Prevented duplicate-image reprocessing by SHA-256 hashing uploads for Cloudinary dedup, reducing redundant storage and inference calls.
- Contributed across a live multi-app production system (Angular SSR frontend, NestJS/GraphQL API, admin panel) as sole developer on an existing codebase — including an async job (Bull queue) that resolves proxy-bid state after every event, a pattern consistent with event-driven backend processing.

### Research Assistant — NJIT, under Prof. Komal Kumari (2025)

- Built the REST API and file-distribution layer for a distributed document-outsourcing research system spanning 4 physical servers, with port-mapped share directories per server (`8080→server1/share1`, `8082→server2/share2`, etc.) and client-scoped access control — contributed to published research.
- Designed 10+ Spring Boot REST endpoints (Java 17) covering document CRUD, keyword/access-control management, and system bootstrap — built API-first, against contracts, before backend integration existed.
- Owned the full Angular frontend consuming those APIs, including session-based file visibility and access-control UI, then wired the service layer to the live distributed backend in a second integration phase.

### Software Engineer Intern — BNP Paribas (2024)

- Delivered 10–12 Jira tickets across a legacy C/.NET-to-Java Spring Boot migration over 5 months, each shipped with unit and integration test coverage, in Agile/Scrum sprints with a 12-person team.
- Built an internal Jira-tracking tool from scratch (Spring Boot REST API + Angular frontend) with full CRUD and CSV/Excel export, adopted by the full 12-person team for daily activity logging.

## Projects

### Outfitted — AI Personal Styling Assistant
github.com/talaviyakhushi/outfitted

- Built a Python/FastAPI backend orchestrating four OpenAI models in one pipeline (gpt-4o vision for tagging, gpt-4o-mini for intent extraction, gpt-4o for chat, text-embedding-3-small for retrieval), with pgvector-backed semantic search over user-scoped wardrobe data (PostgreSQL/Supabase).
- Improved retrieval reliability with gap-fill logic (secondary targeted queries for missing item categories) and a starvation fallback that passes the full wardrobe to the model when initial retrieval returns too few results.

## Skills

**Languages:** Python, Java, TypeScript, JavaScript, SQL, HTML5, CSS3
**AI / ML:** OpenAI API (gpt-4o, gpt-4o-mini, text-embedding-3-small), model serving via REST APIs, RAG pipelines, vector embeddings, prompt engineering
**Cloud / Infra:** AWS (EC2, S3, Amplify, RDS), Docker, GitHub Actions, CI/CD, systemd deployment
**Backend / Frameworks:** Spring Boot, Spring MVC, JPA/Hibernate, FastAPI, NestJS, Node.js
**Databases:** PostgreSQL, MySQL, MongoDB, Supabase (pgvector), AWS RDS
**Tools & Practices:** Git, Maven, JUnit, REST APIs, Agile/Scrum, Postman

## Education

**New Jersey Institute of Technology** — M.S. Computer Science (May 2026)
