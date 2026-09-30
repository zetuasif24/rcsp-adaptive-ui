RCSP — Claude Project Context Page 1
RCSP — Claude Project Context
Rural Community Service Portal
Experimental platform for the thesis:
Adaptive Low-Bandwidth User Interface for Web Applications in Rural Environments
Use: This document is the long-term context/specification for the Claude coding agent. The RCSP portal is the
experimental platform; the adaptive low-bandwidth UI approach and its evaluation are the research focus.

RCSP — Claude Project Context Page 2
1. MASTER PROJECT CONTEXT — PASTE INTO CLAUDE
Project: Rural Community Service Portal (RCSP)
Thesis: Adaptive Low-Bandwidth User Interface for Web Applications in Rural Environments
RCSP is a controlled experimental web application for implementing and evaluating a real-time, network-aware
adaptive user interface under constrained network conditions. RCSP itself is not the main research contribution. The
research contribution is the adaptive low-bandwidth UI approach and its experimental evaluation.
The application must support two comparable conditions using the same core functionality, backend, database, and
comparable content: (1) Conventional UI, a controlled non-adaptive baseline; and (2) Adaptive UI, a network-aware
interface/resource adaptation condition.
The two conditions will be evaluated under controlled network environments such as 2G, 3G, 4G, and Wi-Fi.
Performance measurements will include First Contentful Paint (FCP), page load time, data transferred, and HTTP/API
request count. Usability measurements will include task completion time, task success rate, perceived responsiveness,
and SUS/Likert-style ratings.
Use React + Vite + Tailwind CSS for the frontend, Django + Django REST Framework for the backend, and
PostgreSQL for persistence. Keep the application small, modular, measurable, and research-oriented. Do not add
unnecessary product features.
Agent rules
• Do not build a huge portal. Keep scope controlled.
• Do not remove the conventional baseline.
• Do not make the adaptive version a different application.
• Keep adaptation rules configurable and documented.
• Prefer reusable components and measurable behavior.
• Ask before major architectural changes.
• Do not invent research results or unsupported novelty claims.
• Always distinguish the RCSP prototype from the thesis contribution.

RCSP — Claude Project Context Page 3
2. RESEARCH FOUNDATION
Problem statement
Modern web applications often assume stable and sufficiently fast internet. Rural users may face low bandwidth,
unstable connectivity, high latency, expensive mobile data, and resource-constrained devices. Heavy web resources
can therefore cause slow loading and poor usability.
Research question
Does a real-time, network-aware adaptive user interface significantly improve performance and usability of
web applications compared to a conventional (non-adaptive) interface, under low-bandwidth and
rural-simulated network conditions?
Hypotheses
• H1: The adaptive UI will show significantly lower Page Load Time, FCP, and data transferred than the conventional
UI under 2G/3G conditions.
• H2: Users will report significantly higher perceived responsiveness and usability (SUS score) with the adaptive UI
than with the conventional UI under the same constrained network conditions.
Objectives
1 Objective 1 — Propose an Adaptive UI Approach: Establish a conventional baseline and develop a real-time
network-aware adaptive UI with measurable outcomes such as FCP, data transferred, and HTTP/API requests.
2 Objective 2 — Bandwidth Optimization: Implement image loading optimization, lazy loading, resource
prioritization, caching where appropriate, and related bandwidth-saving techniques using modern web technologies.
3 Objective 3 — Performance Evaluation: Compare adaptive and conventional interfaces using performance and
usability metrics under simulated 2G/3G/4G/Wi-Fi conditions.

RCSP — Claude Project Context Page 4
3. SCOPE AND BOUNDARIES
Included
• Adaptive low-bandwidth web UI development.
• Network condition detection/interpretation.
• Automatic UI/resource adaptation.
• Bandwidth optimization.
• Conventional baseline implementation.
• Performance and usability evaluation.
• Controlled network simulation/throttling.
• Adaptive vs conventional comparison.
Excluded from the core research
• New network protocols or communication technologies.
• Hardware/network-infrastructure improvements.
• Backend/database optimization as the primary topic.
• Native Android/iOS development.
• AI/ML bandwidth prediction.
• Unnecessary enterprise portal features.
Backend optimization may be used for functionality, but the primary research focus remains
client-side/user-interface adaptation under network constraints.

RCSP — Claude Project Context Page 5
4. RCSP APPLICATION SPECIFICATION
Purpose
RCSP represents a rural community service portal where users can discover services, read announcements, view
service details, search information, and submit simple service applications.
Core pages
• Home — introduction, popular services, latest announcements.
• Services — searchable/listed community services.
• Service Details — description, eligibility, requirements, processing information, application action.
• Announcements — service/community notices.
• Application — simple service-request form.
• Search — services and announcements.
• Profile — user information and submitted applications.
Prototype service categories
• Health Services
• Education Support
• Agricultural Assistance
• Social Assistance
•
Identity/Documentation Information
Use clearly marked prototype/demo data unless real data sources are later approved.

RCSP — Claude Project Context Page 6
5. INITIAL DATA MODEL
User
id, name, email, password/auth reference, phone, role, created_at
Service
id, name, description, category, icon/image reference, requirements, processing_time, is_active, created_at
Announcement
id, title, description, image reference, published_at, is_active
Application
id, user, service, full_name, phone, address/description fields, status, submitted_at
Application status
PENDING → PROCESSING → APPROVED / REJECTED
Do not add additional models unless they support a clear application requirement or research need.

RCSP — Claude Project Context Page 7
6. SYSTEM ARCHITECTURE
High-level architecture
User
↓
React RCSP Web Application
↓
Network Detection / Network Profile
↓
Adaptive UI Engine
↓
UI Controller + Resource Manager
↓
Django REST API
↓
PostgreSQL Database
Experimental conditions
Same RCSP functionality + same backend + same database + comparable content ■ ■■■ Conventional UI ■ ■■■
normal resource loading; no network-aware adaptation ■ ■■■ Adaptive UI ■■■ network-aware resource/UI
adaptation
Adaptive pipeline
NetworkDetector → NetworkProfile → AdaptiveEngine → AdaptationRules → ResourceManager/UI Controller →
RCSP UI
Keep the adaptive engine modular so it can be tested and explained independently.

RCSP — Claude Project Context Page 8
7. ADAPTIVE UI BEHAVIOR
The exact network thresholds must remain configurable until the experimental protocol is finalized.
Profile Example behavior
Fast Full visual content, higher-quality images, normal loading.
Moderate Compressed images, normal UI, lazy loading for non-critical resources.
Slow Lower-resolution/compressed images, prioritize text/critical content, aggressive lazy
loading, defer nonessential resources.
Very slow Minimal/lightweight presentation, essential content first, avoid unnecessary heavy
resources.
Candidate adaptation mechanisms
• Conditional/image-optimized loading.
•
Image compression and modern formats.
• Lazy loading below-the-fold resources.
• Critical resource prioritization.
• Deferring nonessential resources.
• Reducing unnecessary API requests.
• Reducing nonessential animations/effects on constrained networks.
• Lightweight rendering paths while preserving core functionality.
• Caching only where it supports a fair experiment.
The adaptive version must change actual resource/network behavior, not only visual styling.

RCSP — Claude Project Context Page 9
8. EXPERIMENTAL DESIGN
Core comparison
Control: Conventional RCSP UI
Experimental: Adaptive RCSP UI
Application: same functionality
Backend/database: same
Tasks: same
Network condition: same for paired comparisons
Network conditions
• 2G
• 3G
• 4G
• Wi-Fi / normal connection
Performance metrics
• First Contentful Paint (FCP)
• Page Load Time
• Data Transferred
• HTTP/API Request Count
Usability metrics
• Task Completion Time
• Task Success Rate
• Perceived Responsiveness
• SUS score and/or structured Likert ratings
Fairness requirements
• Keep functionality equivalent.
• Use the same content/data where possible.
• Run both modes under the same network profile.
• Use repeated trials rather than one page load.
• Document browser/device/environment settings.
• Do not tune the adaptive version using final results in a way that invalidates the comparison.

RCSP — Claude Project Context Page 10
9. REPOSITORY STRUCTURE
rcsp/ ■■■ frontend/ ■ ■■■ src/ ■ ■ ■■■ components/ ■ ■ ■ ■■■ common/ ■ ■ ■ ■■■ layout/ ■ ■ ■ ■■■
services/ ■ ■ ■ ■■■ announcements/ ■ ■ ■■■ pages/ ■ ■ ■■■ adaptive/ ■ ■ ■ ■■■ NetworkDetector.js ■ ■ ■
■■■ AdaptiveEngine.js ■ ■ ■ ■■■ AdaptationRules.js ■ ■ ■ ■■■ ResourceManager.js ■ ■ ■■■ hooks/ ■ ■ ■■■
context/ ■ ■ ■■■ services/api.js ■ ■ ■■■ assets/ ■ ■■■ package.json ■■■ backend/ ■ ■■■ config/ ■ ■■■
users/ ■ ■■■ services/ ■ ■■■ announcements/ ■ ■■■ applications/ ■ ■■■ api/ ■ ■■■ manage.py ■ ■■■
requirements.txt ■■■ docs/ ■ ■■■ research/ ■ ■■■ architecture/ ■ ■■■ wireframes/ ■ ■■■ experiments/ ■■■
CLAUDE.md ■■■ README.md ■■■ .gitignore
Suggested Git milestones
•
Initial architecture
• React/Vite frontend
• Django/DRF backend
• Database models/APIs
• RCSP baseline UI
• Frontend/backend integration
• Conventional UI
• Network detection
• Adaptive UI engine
• Resource optimization
• Research instrumentation
• Experimental setup

RCSP — Claude Project Context Page 11
10. IMPLEMENTATION ROADMAP
1 Architecture: requirements, architecture, data model, page structure, adaptation strategy.
2 Scaffolding: frontend/backend/database/Git/documentation setup.
3 Backend: models, serializers, APIs, validation, admin.
4 Baseline frontend: all seven core pages.
5 Integration: connect frontend to Django APIs.
6 Conventional condition: freeze a clean non-adaptive baseline.
7 Adaptive condition: network detection, adaptation rules, image/resource optimization, lazy loading, prioritization.
8 Instrumentation: FCP, page load, bytes, request counts, network profile, mode, adaptation decisions.
9 Experimental setup: reproducible 2G/3G/4G/Wi-Fi conditions and tasks.
10 Evaluation: repeated performance measurements and usability testing.
11 Analysis: preserve raw data and produce tables/figures/statistical comparisons.
12 Documentation: architecture, implementation, experiment, results, limitations, conclusion.

RCSP — Claude Project Context Page 12
11. CLAUDE AGENT WORKFLOW
Do not ask the agent to build the entire thesis system in one prompt. Work in controlled phases.
Planning prompt
I am building RCSP (Rural Community Service Portal) as the experimental web application for my thesis,
“Adaptive Low-Bandwidth User Interface for Web Applications in Rural Environments.” Read the project context
in this document. Before writing code, analyze the requirements and propose the architecture, data model,
page structure, adaptive UI architecture, experiment structure, folder structure, and implementation phases.
Do not implement yet. Identify ambiguities that require my approval.
CLAUDE.md prompt
Create a concise CLAUDE.md based on the approved architecture. Preserve the distinction between the RCSP
prototype and the thesis research contribution. Include the stack, scope boundaries, conventional/adaptive
comparison requirement, coding conventions, testing expectations, and research measurement requirements.
Scaffolding prompt
Implement only the approved project scaffolding. Set up React/Vite/Tailwind frontend, Django/DRF backend,
PostgreSQL configuration, environment variables, Git configuration, and documentation. Do not implement
adaptive behavior or unnecessary business features yet. Verify that frontend and backend run successfully.
After each major step, require the agent to report: files changed, what was implemented, tests run, assumptions
made, and the next recommended step.

RCSP — Claude Project Context Page 13
12. DO NOT ADD WITHOUT APPROVAL
• Alternative technology stack.
• Large enterprise features.
• AI/ML bandwidth prediction.
• Native mobile apps.
• Payment, mapping, messaging, social feed, or chatbot features.
• Changes to the research question or hypotheses.
• Removal of the conventional baseline.
• Functionally incomparable adaptive/conventional versions.
•
Invented results or unsupported claims.
• Unlogged/unexplainable adaptation logic.
• Backend optimization that becomes the main experimental variable.
Quality rule
Does it support RCSP functionality? Does it support a fair adaptive-vs-conventional experiment? Can its
effect be measured and explained? If the answer is no, do not add it merely because it is technically interesting.

RCSP — Claude Project Context Page 14
13. EXPECTED DELIVERABLES
Deliverable Purpose
RCSP web application Controlled experimental platform.
Conventional UI Control/baseline.
Adaptive UI Experimental condition.
Adaptive engine Network-aware decision and adaptation.
Performance instrumentation Objective measurements.
Experiment configuration Reproducible network/test setup.
Usability tasks Task time, success, responsiveness, usability.
Raw experiment data Evidence for analysis.
Analysis outputs Tables, figures, statistical comparisons.
Technical documentation Architecture and implementation.
Thesis documentation Connect implementation and findings to the research question.

RCSP — Claude Project Context Page 15
14. SHORT DESCRIPTION FOR CLAUDE'S PROJECT
CREATION FORM
Build RCSP (Rural Community Service Portal), a controlled experimental web application for my thesis,
“Adaptive Low-Bandwidth User Interface for Web Applications in Rural Environments.” The portal will
provide services, announcements, service details, search, user profiles, and simple service applications.
The key research requirement is to implement two comparable conditions: (1) a conventional non-adaptive UI
used as the control/baseline, and (2) a real-time network-aware adaptive UI that changes resource loading and
interface behavior according to network conditions. Both must use the same core functionality, backend, database,
and comparable content so the experiment is fair.
The adaptive approach should use techniques such as image optimization, lazy loading, resource prioritization,
reduced nonessential requests, and lightweight rendering while preserving core functionality. The system must
support controlled evaluation under simulated 2G, 3G, 4G, and Wi-Fi conditions. Measurements will include FCP,
page load time, data transferred, HTTP/API requests, task completion time, task success rate, perceived
responsiveness, and SUS/Likert usability measures.
Use React + Vite + Tailwind CSS for the frontend, Django + Django REST Framework for the backend, and
PostgreSQL for the database. Keep the application small, modular, measurable, and research-oriented. Do not add
unnecessary features. The RCSP portal is the experimental platform; the adaptive low-bandwidth UI approach and
its evaluation are the research focus.
Recommended project name: RCSP — Rural Community Service Portal
Recommended repository name: rcsp-adaptive-ui

RCSP — Claude Project Context Page 16
15. ACCEPTANCE CRITERIA
• The same RCSP tasks work in both conventional and adaptive modes.
• The conventional mode can be held stable as a baseline.
• The adaptive mode reacts to documented network conditions.
• Adaptive behavior changes actual resource/network behavior, not only visual styling.
• Network condition and adaptation mode can be logged.
• Performance metrics can be collected reproducibly.
• Usability tasks are repeatable.
• The network/test environment is documented.
• Raw results are preserved separately from analysis.
• The adaptive engine is modular and explainable.
• The application does not introduce unrelated confounding features.
• Claims can be supported by implementation evidence or experiment results.
Final end state
A researcher should be able to select the same RCSP page/task, run either Conventional or Adaptive mode, apply a
controlled network condition, execute the task, and collect comparable performance and usability evidence.
This document is project context, not a replacement for supervisor approval, final experimental protocol, participant/ethics requirements, or
the final thesis methodology.

