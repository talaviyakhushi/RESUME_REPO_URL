# Fit Report — Software Engineer, Infrastructure @ Baseten

## Overall fit

**Tier:** Stretch
**Verdict:** Too far a stretch for this role - try closer-aligned roles

This role centers on Kubernetes-based inference infrastructure, Go, GPU resource management, and orchestration systems — none of which appear in `resume.md`. Khushi's background is fullstack web development (Angular/NestJS/Spring Boot) with meaningful Python and AI/ML API-integration exposure, plus one research project touching distributed systems, but no container-orchestration or infra-automation-at-scale experience. Honest positioning: apply to fullstack, backend, or AI-product-integration roles first; if pursuing this one, be upfront in interviews about the Kubernetes/Go gap and lean on the Python + distributed-systems + ML-integration evidence that does exist.

## Strong matches

- **Python proficiency (required):** Built Python/FastAPI backend for Outfitted (RAG pipeline, pgvector retrieval, OpenAI API orchestration); Python ML pipeline for Flight Fare Prediction (pandas, scikit-learn).
- **Basic ML concepts / model serving (required):** Integrated gpt-4o vision model serving into a production product (AI Price Estimator) — image → model inference → structured output → persistence, plus a second gpt-4o/gpt-4o-mini/embedding pipeline in Outfitted. Direct, hands-on exposure to calling and serving ML model inference in an application.
- **Distributed systems concepts (required):** NJIT research project (DBO) — REST API and file-distribution layer across 4 physical servers with port-mapped share directories and client-scoped access control; published research system.
- **Containerization-adjacent / cloud infra (tools/stack):** Docker, AWS (EC2, S3, Amplify), GitHub Actions CI/CD — used to deploy and run the AI Price Estimator backend (JDK build → SCP → systemd restart on EC2).
- **Infrastructure automation (responsibility):** GitHub Actions CI/CD pipeline automating build and deploy of a live backend service.
- **Monitoring/logging (nice-to-have, partial):** Integrated Microsoft Clarity for user-session identification — analytics/observability tooling, though product-analytics rather than infra-monitoring in nature.
- **Collaboration/communication (required):** Sole developer on a live production codebase (Forty7) coordinating with existing team/business stakeholders; Agile/Scrum delivery in a 12-person team at BNP Paribas.

## Gaps

- **Kubernetes and containerization (required):** No Kubernetes experience anywhere in `resume.md`. Docker experience exists but not orchestration at cluster scale.
- **Go (plus, but a core team language per JD):** No Go in skills or experience — all backend work is Java (Spring Boot) or TypeScript (NestJS).
- **Inference orchestration / GPU resource management (example initiatives):** No experience with multi-node inference, GPU fractional allocation, or capacity management systems.
- **Infra-specific monitoring/logging tools (e.g., Prometheus, Grafana, ELK):** Not present; only product-analytics tooling (Microsoft Clarity) is evidenced.

## Do not add

- Go language proficiency
- Kubernetes / container orchestration
- GPU infrastructure (B200/H100, fractional GPU serving)
- Multi-cloud capacity management
- Prometheus/Grafana or other infra monitoring stacks
- Multi-node inference systems
