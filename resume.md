# Khushi Talaviya — Master Profile

> Single source of truth for all resume generation. Read this fully before generating any resume.
> Do not modify unless Khushi explicitly asks.
>
> Sections marked *Derivation*, "Context for tailoring", and "Bullet variants" are guidance for
> the tailoring agent — use them to pick and phrase content, but never copy them verbatim into
> `tailored-resume.md`.

---

## Contact

- **Email:** khushitalaviya0912@gmail.com
- **LinkedIn:** linkedin.com/in/khushitalaviya
- **GitHub:** github.com/talaviyakhushi
- **Portfolio:** khushitalaviya.vercel.app
- **Location:** New York, NY

---

## Education

**New Jersey Institute of Technology** — Newark, NJ
M.S. Computer Science | Completed May 2026 | GPA: 3.8

(Degree is COMPLETED — never phrase as "completing", "pursuing", or "expected".)

---

## Skills

**Languages:** Java, Python, TypeScript, JavaScript, SQL, HTML5, CSS3
**Frameworks / Libraries:** Spring Boot, Spring MVC, JPA/Hibernate, Angular, NestJS, React, FastAPI, Node.js, TailwindCSS, Angular Material, RxJS, NGXS, Zustand, Apollo GraphQL, Spring RestTemplate
**Databases:** MySQL, PostgreSQL, MongoDB, Supabase (pgvector), AWS RDS
**Cloud / DevOps:** AWS (Amplify, EC2, RDS, S3), Docker, GitHub Actions, CI/CD, Cloudinary, Supabase
**Testing / Tools:** JUnit, Git, Maven, Postman, Jira, Figma
**Practices:** Agile/Scrum, REST and GraphQL API design, unit and integration testing

(Classification note for the agent: keep categories semantically correct in
tailored output — Agile/Scrum and API design are Practices, never Tools;
JUnit is a testing framework; REST APIs is not a tool.)

(No "AI / ML" skills category — OpenAI API usage is real project work (see
Outfitted, AI Price Estimator) but calling it out as a Skills-section
category overstates it; it's API integration, not ML expertise. OpenAI/RAG/
embeddings may still appear in project and experience bullets where the work
itself is the evidence, just never as a standalone Skills line.)

---

## Experience

### Forty7 — Software Developer Co-op
**Location:** New York, NY
**Duration:** January 2026 – May 2026
**Stack:** Angular 18, TypeScript, NGXS, Apollo GraphQL (codegen), NestJS, TypeORM, PostgreSQL, AWS (S3, SES, SNS), Angular SSR, Klaviyo API, WATI (WhatsApp Business API), Microsoft Clarity, SCSS
**Project context:** Forty7 is a live diamond and gemstone auction platform with 100 users — Angular SSR frontend, NestJS/GraphQL API, Angular admin panel. Khushi joined an existing production codebase and contributed across all three apps: third-party marketing/analytics integrations, guest access architecture, new pages from scratch, GraphQL schema extensions, and NestJS backend fixes.

---

**The work:** Delivered features across frontend, NestJS backend, and admin panel in a real production environment with live users. Owned third-party integrations end-to-end (browser SDK → backend service → GraphQL), fixed auth race conditions in NGXS state management, built multiple pages from scratch, and extended GIA GraphQL schema to support new listing UI.

---

**Analytics & Marketing Integrations (full-stack):**
- Built `KlaviyoService` from scratch in Angular — `identify()` and `track()` calls injected into both individual and business signup flows post-success; SSR-safe (platform/browser check guards all `window` access)
- Fixed NestJS Klaviyo subscription flow: handled HTTP 409 (duplicate profile) by extracting existing profile ID from error response and re-routing to subscribe/add-to-list — previously silently failed on duplicate signups
- Integrated Microsoft Clarity user identification: for logged-in users, calls `clarity('identify', ...)` with user ID and email; for guests, reads and base64-decodes the `__kla_id` Klaviyo cookie to surface email as a custom Clarity label — cross-tool identity stitching without requiring authenticated state
- *Derivation:* Cookie decode path: `JSON.parse(atob(cookieValue))` → extract `$email` field — non-trivial guest identity resolution that doesn't touch any auth state

**WATI (WhatsApp Business) Integration (end-to-end):**
- Extended NestJS backend: added `kycTextSentAt` timestamp column to User entity (TypeORM migration), exposed `sendKycText` GraphQL mutation (admin-only, role-guarded), wired through `WatsAppService.kycSupport()` — idempotent: throws `BadRequestException` if message already sent
- Updated WATI message templates across service layer (registration, listing sold, listing unsold) when business renamed templates
- Surfaced KYC trigger action in Angular admin panel business users table — GraphQL mutation wired through NGXS action/state/service chain

**Guest Access Architecture:**
- Reworked auth/guest UX: allowed unauthenticated users to browse lot detail pages, view results tab, interact with WATI widget — removed login gates from paths that don't require authentication
- Fixed auth state race condition on app initialization: added `initialized` boolean to NGXS `AuthStateModel`, dispatched after localStorage token hydration — prevented route guards from evaluating before auth state was ready
- *Derivation:* Root cause was NGXS state reset on logout wiping the `initialized` flag — fixed by excluding `AuthState` from the reset and manually patching token to null instead of full state reset

**Pages Built / Significantly Developed:**
- About Us — dynamic stone carousel backed by extended GIA GraphQL query (`gia-schema.graphql` + `gia-graphql.ts`); each stone linked to corresponding lot listing; full responsive layout from scratch
- Request Access — new route + component scaffolded and wired into `app.routes.ts` and `auth.routes.ts`
- Auctions/Home, How It Works, Sell With Us, FAQs — major markup and layout overhauls; responsive SCSS, updated routing logic
- Updated header nav dynamically based on auth/lot state; added conditional redirect to About Us when no active lots

**Results Tab:**
- Added Results tab to listing/lot UI; extended GIA GraphQL schema with results query; removed old auto-redirect behavior in favor of tab-based navigation

**FCRF Certificate Fix (NestJS + Angular):**
- Fixed response field mapping in `fcrf.service.ts` when upstream certificate API changed format — refactored mapping logic; updated Angular `lot-details` component to display new format correctly

**SEO:**
- Updated Open Graph title and meta description for homepage via `seo-config.ts`

**Bug Fixes:**
- Fixed JWT collision bug: `sign({}, secret)` produced identical tokens for concurrent logins — added `sub: user.id` to payload making every token unique per user
- Fixed inverted filter condition in admin panel copyListing — `!== null || !==` blocked valid lots and allowed invalid ones; corrected to `=== null && ===`

---

**Max Bid (Proxy Bidding) Feature — built end-to-end (do not phrase as "sole developer/owner" in output; "owned end to end" is the ceiling):**
- Built complete proxy bidding system from scratch across API, frontend, and admin panel
- **NestJS/GraphQL API:** New `MaxBid` TypeORM entity with unique constraint `(userId, lotId)` — one active max bid per user per lot; TypeORM migration with FK constraints and rollback; `MaxBidModule` with service, resolver, validators; `setMaxBid` mutation (business users only, role-guarded)
- **Bid validation:** `MaxBidAmountValidator` — validates amount ≥ current highest bid × 1.03 rounded up to nearest $100 (or lot start price if no bids); blocks non-business accounts; `NoActiveMaxBidValidator` — blocks manual bid if user has active max bid that hasn't been outbid, preventing collision between proxy and manual bidding
- **Proxy resolution engine** (`resolveMaxBid` Bull queue job): fires after every new bid; fetches all max bids for lot sorted by amount desc; determines proxy bid amount from runner-up's max, current highest bid, and winner's ceiling; places proxy bid via `createProxyBid`; handles all notification paths; suppresses outbid notifications for max bid holders while proxy is active
- **Bid increment rule:** updated from flat 2% to 3% rounded up to nearest $100 — `Math.ceil((amount * 1.03) / 100) * 100`
- **Notifications + email + WATI:** `MaxBidSet` notification type added to enum (DB migration to extend PostgreSQL enum); `max-bid-set.hbs` transactional email template; WATI `maxBidSet()` WhatsApp confirmation message
- **Angular frontend:** extended `ModalPlaceBid` component — toggle between manual bid and max bid modes (285 lines net added); new `SetMaxBid` NGXS action and state; `setMaxBid` GraphQL mutation wired through `BidService`; `MaxBidSet` notification type mapped in notification display utils
- **In production:** live across the last 3 auctions (5 lots each — 15 lots)
- *Derivation:* Outbid notification suppression required modifying `BidService.create()` — checks if outbid user has active max bid before sending email/WATI/push; avoids spamming users immediately re-bid by proxy

---

**AI Price Estimator (separate deployed product, built end-to-end — same phrasing rule: no "sole developer/solo" in output):**
- Built standalone AI luxury resale pricing tool for Forty7: Angular 19 + Spring Boot 3.5 + Java 21 + MySQL 8 + gpt-4o vision — live in production (AWS Amplify + EC2)
- Image upload → Cloudinary (SHA-256 dedup as `public_id`) → gpt-4o vision strict JSON classification (watch/jewelry/unknown + attribute extraction) → Angular Reactive Form pre-fill via `ngOnChanges/@Input` → domain-tuned gpt-4o pricing prompt → estimate persisted to MySQL
- reCAPTCHA v2 gate on both estimation endpoints (`/estimate/jewelry`, `/estimate/watch`) — backend verifies token via Google siteverify before any OpenAI call
- CI/CD: GitHub Actions → JDK 21 → `mvn -B -DskipTests package` → SCP jar to EC2 → `systemctl restart estimator-backend`; frontend auto-deploys via AWS Amplify on push
- **Accuracy validation:** benchmarked estimates on 3,000+ items against listings on luxury resale marketplaces (The RealReal, LoupeThis) — model showed 90% accuracy
- **Usage + latency:** used by ~100 people in production; image upload + vision scan completes in ~5 seconds, final price estimate returns in 1–2 seconds after user confirms details
- *Derivation:* Watch completeness check before calling OpenAI — if only brand + material known (no reference, movement, condition) returns "need more info" to save API cost
- *Derivation:* SHA-256 dedup in Cloudinary = same image never uploaded twice; `MessageDigest.getInstance("SHA-256")` on file bytes used as `public_id`

---

**Bullet variants by role type** *(pick 2–3 most relevant per JD)*

*Fullstack / SWE:*
- Built proxy bidding (max bid) system end-to-end at Forty7: TypeORM entity + migration, NestJS GraphQL mutation with custom class-validator constraints, Bull queue processor for proxy resolution logic, and Angular modal UI with NGXS state — business-critical auction feature owned end to end
- Contributed across Angular SSR frontend, NestJS/GraphQL backend, and admin panel at Forty7 — built WATI WhatsApp integration end-to-end (TypeORM entity → GraphQL mutation → admin UI), wired Klaviyo and Microsoft Clarity analytics, and architected guest access flow for a live auction platform
- Built AI price estimator end-to-end (Angular 19 + Spring Boot 3.5 + gpt-4o vision, live in production): photo upload → AI classification + form pre-fill → domain-tuned pricing prompt → MySQL persistence, with reCAPTCHA gate and GitHub Actions CI/CD

*Backend / API:*
- Implemented proxy bid resolution as a Bull queue job: determines bid amount from ranked max bids, handles all outbid notification paths, and suppresses redundant notifications for max bid holders — designed idempotent and collision-safe with manual bidding
- Extended NestJS/GraphQL API at Forty7: added role-guarded mutations, TypeORM entity columns, idempotent WhatsApp message sending, and fixed upstream FCRF certificate API response mapping
- Fixed NGXS auth state race condition on app init: added `initialized` flag to prevent route guards from evaluating before localStorage token hydration completed
- Built Spring Boot 3.5 backend for AI estimator: gpt-4o vision classification, Cloudinary upload with SHA-256 dedup, reCAPTCHA verification, MySQL persistence, deployed to EC2 with systemd + GitHub Actions

*Frontend / Angular:*
- Built About Us page with GraphQL-backed dynamic carousel, Results tab with extended GIA schema, and Request Access page from scratch in Angular 18 with SSR; reworked guest UX across lot detail, results, and header navigation
- Built SSR-safe KlaviyoService; implemented Microsoft Clarity user identification using Klaviyo cookie decoding for guest sessions — cross-tool identity without authenticated state
- Built Angular 19 estimator frontend: gpt-4o vision analyze flow, `ngOnChanges`-driven form pre-fill from AI response, reCAPTCHA render + token handling, RxJS `retry(1)` + `timeout(30000)` on analyze call

*AI / product:*
- Built and shipped AI luxury resale pricing tool at Forty7 (owned end to end, live production): gpt-4o vision classifies watch/jewelry from photo and extracts attributes → domain-tuned pricing prompt with conservative secondary-market constraints → USD price range returned and persisted — 90% accuracy benchmarked on 3,000+ items against The RealReal and LoupeThis listings

*Analytics / Integrations:*
- Integrated Klaviyo JS tracking and Microsoft Clarity identification in Angular SSR app; wired WATI WhatsApp Business API in NestJS with idempotency guard; fixed Klaviyo backend subscription flow for duplicate profile edge case

---

### NJIT — Research Assistant (under Prof. Komal Kumari)
**Location:** Newark, NJ
**Duration:** April 2025 – September 2025
**Stack:** Angular 15, TypeScript, Java 17, Spring Boot 3.4.5, REST APIs, Maven, Node.js, Gson, Jackson
**System context:** DBO (Document-Based Outsourcing) — document outsourcing research system. Documents distributed across 4 servers; clients search by keyword with access control per client. Khushi owned the full frontend and REST API layer. The research was published; the system was validated at 500K-document scale for the paper (scale testing performed after Khushi's involvement ended — frame as "contributed to published research", not as tests she ran).

---

**The work:** Built the complete Angular dashboard and REST API layer for a document outsourcing research system. Owned everything the user touches — DBO interface, client search interface, and all Spring Boot endpoints the frontend calls. Delivered two phases: API-first frontend design against contracts, then full backend integration.

---

**Angular Frontend (doc-dashboard — sole owner):**
- Built full Angular 15 app from scratch: DBO dashboard + client search interface, routing, service layer, dialogs, data models
- DBO dashboard: bulk file/directory upload, session-based file visibility (auto-expires 30 min), file add/delete, client ID management
- Keyword management UI: view all extracted keywords post-processing, grant/revoke keyword access per client — Access Control Matrix interaction without exposing internals
- Client search view: keyword-based document search ("Google search" style), file open/download visualization
- *Derivation:* Session-expiry file display = no persistent plaintext exposed in UI — deliberate design matching the system's privacy model
- *Derivation:* Advisor explicitly required going beyond dropdowns — implemented drag-and-drop interactions and Apple Watch-style keyword bubble UI. Visual design was a graded deliverable, not an afterthought.

**Spring Boot REST API layer (added to provided codebase):**
- Added `OutSourceController` — 10+ REST endpoints wiring frontend to backend services:
  - `POST /api/upload`: bulk upload, per-client folder organization, numeric file ID assignment
  - `GET /api/documents`, `DELETE /api/documents/{clientId}/{fileId}`: document CRUD
  - `GET /api/all-keywords`, `DELETE /api/keywords/{keyword}`: keyword management
  - `POST /api/access/grant`, `POST /api/access/revoke`: client-keyword ACL mutations
  - `POST /api/initialize`, `GET /api/client-map`, `POST /api/update-keyword-map`: system bootstrap and mapping management
- Added `FileReceiverController` — `POST /upload` port-mapped to server-specific share directories (`8080→server1/share1`, `8082→server2/share2`, etc.) enabling distributed share storage across 4 servers
- JSON-based persistent mappings for client IDs, file metadata, and access permissions; CORS configured for Angular dev server
- *Derivation:* API-first Phase 1 — built entire frontend against contracts before backend existed. Forced clean interface separation.

**Integration (Phase 2):**
- Studied provided backend code to understand data shapes and API contracts
- Wired Angular service layer to live Spring Boot endpoints
- Reorganized codebase: merged outsource + grant-revoke modules into unified DBO package without touching existing logic

---

**Bullet variants by role type** *(pick 2–3 most relevant per JD)*

*Fullstack / SWE:*
- Built full Angular 15 dashboard and 10+ Spring Boot REST endpoints for a privacy-preserving document outsourcing research system — delivered API-first frontend design and full backend integration across two phases
- Designed Angular service layer against Spring Boot APIs for a distributed cryptographic document system: session-based file visibility, client-keyword access control, bulk upload with per-client organization

*Frontend / UI:*
- Built Angular 15 doc-dashboard from scratch for a research cryptography system — drag-and-drop interactions, Apple Watch-style keyword bubble UI, session-expiry file visibility, multi-view routing for DBO and client perspectives
- Visual design was an explicit deliverable: keyword browsing, access grant/revoke flows, and client-side document search all built for usability alongside functional correctness

*Backend / API:*
- Added 10+ REST endpoints to a Java 17 Spring Boot research system covering document CRUD, keyword management, client-keyword ACL, and port-mapped multi-server file distribution across 4 servers

---

### BNP Paribas — Software Engineer Intern
**Location:** Mumbai, India
**Duration:** January 2024 – July 2024
**Stack:** Java, Spring Boot, Angular, REST APIs, Maven, Git, JUnit, Agile/Scrum
**Project context:** Legacy financial risk-calculation engine being migrated from C and .NET to Java Spring Boot (Maven) for maintainability and modern tooling — a large multi-year migration (still ongoing 2+ years after Khushi's departure), delivered by a 12-person team. Khushi contributed across the full migration — backend logic, frontend, CSS — and also built an internal developer productivity tool from scratch in the onboarding phase.

---

**The work:** Started with two months of onboarding + internal tooling, then transitioned to sprint-based feature delivery on the core migration project. Delivered 10–12 Jiras across backend, frontend, and styling — with unit and integration tests for each.

---

**Jira Tracker Tool (Jan–Feb, sole owner):**
- Built internal team productivity tool during onboarding: form-based Jira logging where each team member records Jiras worked on per date
- Manager view: aggregated table of all team submissions, exportable (CSV/Excel)
- Full CRUD implementation — create, read, update, delete entries
- REST APIs built with Spring Boot; Angular frontend consuming them
- Used by the full 12-person team for daily Jira logging
- *Derivation:* Problem was real — tracking daily Jira activity across a team was manual and scattered. Tool centralized it. Saved meaningful manager time each sprint cycle.
- *Derivation:* Onboarding project served double purpose: learned the stack (Spring Boot + Angular) by shipping something, not just reading docs.

**Core Migration Project (March–July):**
- Worked on 10–12 Jiras across 5 months: mix of backend logic changes (Java Spring Boot), frontend changes (Angular), and CSS styling fixes
- Each Jira shipped with unit tests (JUnit) + additional test file covering integration or edge cases
- Participated in sprint planning, daily standups, retrospectives — Agile/Scrum delivery
- Used Git for version control; deployed changes to dev environment
- *Derivation:* C/.NET → Java Spring Boot migration = not greenfield. Required reading existing C/.NET business logic, understanding intent, then re-implementing correctly in Java idioms. Higher cognitive load than typical feature work.
- *Derivation:* Maven as build system — part of modernization rationale alongside Spring Boot. Standard enterprise Java toolchain choice.
- *Derivation:* Writing a test file per Jira (not per codebase) = disciplined habit. Ensures every change has a corresponding regression harness regardless of coverage elsewhere.

---

**Bullet variants by role type** *(pick 2–3 most relevant per JD)*

*Fullstack / SWE:*
- Delivered 10–12 Jiras across backend (Java Spring Boot), frontend (Angular), and CSS on a C/.NET → Java migration at BNP Paribas — each Jira shipped with unit tests and integration test coverage
- Built internal Jira tracking tool from scratch (Spring Boot REST APIs + Angular): form-based daily logging per team member, manager-facing aggregated table with export — eliminated manual sprint reporting

*Backend / Java:*
- Contributed backend logic changes in Java Spring Boot across a legacy C/.NET → Java migration; implemented unit and integration tests per Jira in Agile sprint delivery at BNP Paribas
- Built REST API layer for internal team productivity tool using Spring Boot, reducing manual Jira activity tracking overhead for managers

*Frontend:*
- Delivered Angular frontend changes and CSS fixes across 10–12 Jiras in Agile sprints at BNP Paribas; built Angular UI for internal Jira tracker tool consuming Spring Boot REST APIs

*Testing / quality:*
- Maintained unit test + integration test file per Jira across 5 months of sprint delivery on a Java Spring Boot migration — disciplined per-change test coverage in an Agile team environment

---

## Projects

### Outfitted — AI Personal Styling Assistant
**Date:** March 2026
**Repo:** https://github.com/talaviyakhushi/outfitted
**Stack:** React 18, Vite, TailwindCSS, React Router, Zustand, FastAPI (Python), PostgreSQL (Supabase), pgvector, OpenAI API (gpt-4o, gpt-4o-mini, text-embedding-3-small), Cloudinary, rembg, Supabase Auth
**Tags:** AI, agentic, RAG, fullstack, personal project
**Status:** In progress, working locally — not yet deployed; tested by 10 users who uploaded 50–100 wardrobe items each (500+ items total)

**What it does:**
AI-powered personal wardrobe assistant. User uploads clothing photos → gpt-4o vision auto-classifies and embeds each item → chat interface retrieves relevant wardrobe pieces via semantic search → gpt-4o streams structured outfit suggestions → frontend renders 5-slot visual collages (top, bottom, shoes, accessories, jewelry).

**Technical depth — every layer:**

*Image upload + auto-classification (`ai_tagging_service.py`):*
- gpt-4o vision classifies each uploaded item: category, subcategory, color, occasion, season — strict JSON-only prompt, validated against enum whitelists, retry up to 2x on invalid response
- rembg removes background before Cloudinary upload for clean collage rendering
- text-embedding-3-small embedding generated from classification: `"A {color} {subcategory} in the {category} category. Suitable for {occasion} occasions and {season} weather"` → stored in `wardrobe_items.embedding vector(1536)` (pgvector)

*Intent extraction (`intent_service.py`):*
- gpt-4o-mini with JSON schema validation classifies each user message using last 4 conversation turns
- Extracts: `request_type` (outfit_request/greeting/off_topic), `is_vague`, `occasion`, `formality` (casual/smart_casual/formal), `weather_sensitivity`, `categories_needed`, `specific_items_mentioned`
- Vague requests short-circuit to clarification question before hitting retrieval

*RAG retrieval (`retrieval_service.py`):*
- Builds context-enriched query from intent fields + user profile (gender, body type, fit, style vibes) + raw message — embeds with text-embedding-3-small
- pgvector cosine similarity search via `match_wardrobe_items_v2` Supabase RPC (`<=>` operator), user-scoped, top-k=20
- Category gap-fill: if required categories absent from primary retrieval, runs targeted secondary RPC per missing category
- Weather → season filter: `warm→summer`, `cold/chilly/rainy→fall/winter`
- Retrieval starvation fallback: <8 results or missing tops/bottoms/shoes → full wardrobe passed to LLM
- Post-retrieval: merges full accessories + jewelry inventory regardless of similarity score

*Streaming chat + outfit generation (`ai_chat_service.py`):*
- Dynamic system prompt: wardrobe formatted as `"Item {i}: {color} {subcategory} ({category}, {occasion}, {season})"` + profile block injected per request
- gpt-4o streaming via SSE; chunks accumulated from `delta.content`
- Model outputs structured blocks: `OUTFIT_START / LABEL / TOP / BOTTOM / SHOES / ACCESSORIES / JEWELRY / OUTFIT_END`
- Regex parses outfit blocks from stream; fuzzy word-overlap scoring matches model descriptions to actual wardrobe item image URLs
- `OUTFIT_IMAGES` JSON payload appended to stream → frontend renders 5-slot collage per outfit

*Onboarding + auth:*
- 6-step onboarding: gender, height, body type, fit preference, style vibes, occasions, skin tone, colors, budget → `user_profiles` table, hydrates on edit
- Supabase Auth JWT frontend; backend validates Bearer token per request

**Context for tailoring:**
- Strong signal for AI/agentic, RAG, fullstack, and product roles
- Real multi-model orchestration: gpt-4o vision (tagging) + gpt-4o-mini (intent) + gpt-4o (chat) + text-embedding-3-small (retrieval) — four OpenAI models in one pipeline
- Retrieval design shows depth: intent-enriched queries, gap-fill logic, starvation fallback — not just "embed and search"
- End-to-end personal project shipped solo and validated with 10 test users: product thinking + engineering execution

---

### Real-Time AI Mock Interviewer
**Date:** February 2026
**Stack:** TypeScript, Node.js, Express, WebSockets, ElevenLabs, Google Gemini, Twelve Labs
**Tags:** AI, real-time, WebSocket, multi-API orchestration, hackathon
**Status:** Shipped — built in 24 hours by a 2-person team

**What it does:**
Real-time voice-driven mock interview platform. User speaks → voice transcribed → Gemini generates interview question/feedback → ElevenLabs synthesizes spoken response → Twelve Labs handles video/code context — all over a single persistent WebSocket connection. Editor state streamed alongside audio for contextual AI follow-up per utterance.

**Technical depth:**

*Pipeline architecture:*
- 3 external APIs orchestrated over one WebSocket: ElevenLabs (voice), Google Gemini (LLM), Twelve Labs (video/code context)
- Full voice-to-code interview loop: speech → transcription → LLM response → TTS — in real time, no polling
- Backend lock prevents concurrent AI responses: one in-flight response at a time, preventing corruption from overlapping streams
- Editor state (code) streamed alongside audio → Gemini receives current code per utterance → contextual follow-ups without manual submission

*Engineering decisions:*
- Single WebSocket connection for all 3 APIs — avoids per-request HTTP overhead, enables low-latency bidirectional flow
- Backend concurrency lock = simple boolean flag — prevents race condition where user speaks again before previous response completes
- Built and shipped in 24 hours

**Bullets (use as-is or adapt):**
- Delivered full voice-to-code interview pipeline in 24 hours by orchestrating 3 external APIs over single WebSocket connection
- Prevented concurrent response corruption by implementing backend lock ensuring one AI response in-flight at a time
- Achieved real-time code visibility by streaming editor state alongside audio enabling contextual AI follow-up per utterance

**Context for tailoring:**
- Strong signal for real-time systems, WebSocket, AI integration, hackathon execution speed
- Shows multi-API orchestration under time pressure — different signal than Outfitted (depth) vs this (speed + systems thinking)
- Good for roles that mention real-time features, voice/audio, or AI tooling

---

### Flight Fare Prediction — ML Regression
**Stack:** Python, pandas, NumPy, scikit-learn (KNN, Decision Tree, Random Forest, RandomizedSearchCV), seaborn, matplotlib
**Tags:** ML, data science, regression, Python, EDA
**Status:** Personal/self-learning project, pre-NJIT

**What it does:**
End-to-end ML pipeline predicting Indian domestic flight fares. Raw dataset (13,000+ records) → EDA → feature engineering → model comparison (3 algorithms) → hyperparameter tuning → Random Forest achieving 82% R².

**Technical depth:**

*Dataset:*
- 10,683 train + 2,671 test rows; features: Airline, Date_of_Journey, Source, Destination, Route, Dep_Time, Arrival_Time, Duration, Total_Stops, Additional_Info, Price (target, range ₹1,759–₹79,512)

*EDA + Visualizations:*
- Airline frequency countplot (ranked by volume)
- Max price per airline — Jet Airways Business topped at ₹79,512
- Weekend vs weekday price comparison per airline (bar plot with hue)
- Correlation heatmap across all engineered features

*Feature Engineering:*
- Date_of_Journey → Journey_month, Journey_date (year dropped — single value, zero variance)
- Dep_Time, Arrival_Time → Dep_hour, Dep_min, Arrival_hour, Arrival_min (string split)
- Duration → total minutes: parsed "Xh Ym" format; edge case handled — two records had "5m" only (minutes-only duration), corrected manually before int cast
- Total_Stops → "non-stop" → 0, "X stops" → integer
- Dropped: Route, Additional_Info (low signal); raw string columns dropped post-extraction
- Missing values: Price (2,671 test rows) filled with mean; one null Total_Stops filled with mode

*Encoding:* LabelEncoder on Airline, Source, Destination

*Model comparison:*
| Model | R² |
|---|---|
| KNN Regressor | 58.75% |
| Decision Tree | 66.25% |
| Random Forest | 80.22% |

*Hyperparameter tuning (RandomizedSearchCV on Random Forest):*
- Search space: n_estimators [100–250], max_features ['auto','sqrt'], max_depth [5–20], min_samples_split [2–100], min_samples_leaf [1–10]
- 3-fold CV, 10 candidates, n_jobs=-1
- Best: n_estimators=200, max_depth=15, min_samples_leaf=2
- **Final R²: 82.27%** | MAE: 1,138 | RMSE: 1,922

**Context for tailoring:**
- Full ML pipeline from scratch: EDA → feature engineering → model selection → tuning
- Messy real-world data: mixed datetime formats, free-text duration strings, edge cases
- Model selection discipline: compared 3 algorithms before tuning the best
- Strong signal for data science, ML engineering, and Python-heavy analytics roles

**Bullet variants by role type** *(pick 2–3 most relevant per JD)*

*ML / Data Science:*
- Predicted Indian domestic flight fares with 82% R² by engineering 12 features from raw datetime/string columns and tuning Random Forest via RandomizedSearchCV across 5 hyperparameters on 13,000+ records
- Improved baseline Random Forest R² from 80% to 82% through 3-fold cross-validated hyperparameter search (n_estimators=200, max_depth=15); benchmarked against KNN (59%) and Decision Tree (66%)

*Python / Data Engineering:*
- Cleaned and feature-engineered 13,000+ flight records in pandas — parsed duration strings, extracted datetime components, corrected edge-case malformed entries — reducing nulls to zero before modeling
