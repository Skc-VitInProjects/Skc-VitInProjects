<h2 id="featured-projects">Featured Projects</h2>

<img src="assets/dividers.svg" width="100%"/>

<p align="center"><img src="assets/boss-card.svg" width="100%"/></p>

<br/>

### Mission 01 — HangOut · Full-Stack Social Media Platform

**Stack:** React.js · Node.js · Express.js · MongoDB · Redux Toolkit · Clerk · Inngest · Multer · ImageKit CDN
**Repository:** [github.com/Skc-VitInProjects/HangOut](https://github.com/Skc-VitInProjects/HangOut)
**Live Demo:** Not publicly deployed — runnable locally from the repository

| | |
|---|---|
| **Overview** | A MERN-stack social platform with chronological activity feeds, connection management, and ephemeral 24-hour stories governed by custom privacy permissions. |
| **Architecture** | React + Redux Toolkit client talking to an Express/MongoDB API; authentication delegated to Clerk; background jobs (story expiration, scheduled email retries) handled by Inngest workers decoupled from the request/response cycle. |
| **Engineering Decisions** | Chose **Server-Sent Events** over WebSockets for real-time messaging — the app only needed server-to-client push, so SSE avoided the handshake and connection-management overhead of a full-duplex protocol. An in-memory connection registry tracks active listeners per user. |
| **Challenges** | Coordinating ephemeral content (24-hour stories) with asynchronous cleanup without blocking the request path — solved by moving expiration into scheduled Inngest functions instead of cron-polling the database. |
| **Features** | Activity feeds · real-time connection requests · 24-hour stories with privacy scoping · media uploads via Multer + ImageKit |
| **Lessons Learned** | SSE is a strong default for one-directional real-time updates — bidirectional protocols carry cost that isn't always justified by the use case. |

<br/>

### Mission 02 — Divyam · API Inspector & Bug Reproduction Assistant

**Stack:** React · TypeScript · Manifest V3 · IndexedDB · Zod · Vitest
**Repository:** [github.com/Skc-VitInProjects/Divyam](https://github.com/Skc-VitInProjects/Divyam)
**Live Demo:** Chrome DevTools extension — load unpacked from the repository

| | |
|---|---|
| **Overview** | A local-first Chrome DevTools extension that captures, filters, and inspects live REST/GraphQL network traffic directly inside browser debugging workflows. |
| **Architecture** | Manifest V3 service-worker architecture with a React-based DevTools panel; a modular Repository pattern isolates persistence (IndexedDB) from capture and export logic, backed by automated Vitest suites. |
| **Engineering Decisions** | Built offline-first with **IndexedDB** session persistence so developers can save, replay, and diff failing vs. successful API payloads across sessions without a backend dependency. |
| **Challenges** | Safely exporting captured requests as cURL/Markdown without leaking credentials — addressed with **Zod**-schema-driven redaction applied before any export is generated. |
| **Features** | Live REST/GraphQL traffic capture · request delta comparison · credential-redacted cURL/Markdown export · offline session storage |
| **Lessons Learned** | Designing the redaction schema before the export format kept sensitive data out of every downstream artifact by construction, rather than by after-the-fact filtering. |

<br/>

### Mission 03 — ConfirmStay · Accommodation Listing & Review Platform

**Stack:** Node.js · Express.js · MongoDB · Mongoose · Passport.js · Cloudinary · Joi
**Repository:** [github.com/Skc-VitInProjects/ConfirmStay](https://github.com/Skc-VitInProjects/ConfirmStay)
**Live Demo:** Not deployed — a learning-stage MVC build without a booking flow or production users

| | |
|---|---|
| **Overview** | A full-stack accommodation marketplace built on the MVC pattern, supporting dynamic listing management and user reviews. |
| **Architecture** | Express + EJS server-rendered views, MongoDB via Mongoose, session-based auth through Passport.js, media handled through Cloudinary. |
| **Engineering Decisions** | Enforced **resource-level authorization** on top of authentication — every mutation checks listing ownership server-side, not just whether a user is logged in. |
| **Challenges** | Preventing orphaned reviews when a listing is deleted — solved with Mongoose middleware hooks that cascade cleanup automatically on delete. |
| **Features** | Listing CRUD · review system · Joi-validated input schemas · ownership-scoped authorization |
| **Lessons Learned** | Validation and authorization belong at the schema and middleware layer, not scattered across route handlers — it made the codebase far easier to audit. |

