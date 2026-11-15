<div align="center">

<a href="https://covermelienservices.com"><img src="assets/cover-me-lien-services.jpg" alt="Cover Me Lien Services: A lien-compliance platform that helps California contractors protect their right to get paid." width="100%"/></a>

# Cover Me Lien Services

**A lien-compliance platform that helps California contractors protect their right to get paid.**

[![Live site](https://img.shields.io/badge/Live-covermelienservices.com-f26b2a?style=for-the-badge&logo=googlechrome&logoColor=white)](https://covermelienservices.com) [![Case study](https://img.shields.io/badge/Case_study-shairali.com-111?style=for-the-badge)](https://shairali.com/work/cover-me-lien-services)

SaaS · CoverM Enterprise, LLC · California, USA · Mar 2026 – Oct 2026

</div>

> [!NOTE]
> This repository is a **showcase**. The source code is private and belongs to the client, so this page documents what I built, how it works and the stack behind it. Screenshots are from the live product.

<p align="center"><img src="assets/tour.gif" alt="Cover Me Lien Services product tour" width="100%"/></p>

## Overview

Construction-lien document preparation and deadline tracking for contractors, subcontractors, suppliers and law firms, with online intake, payments, a client portal and an admin back office.

| | |
|---|---|
| **Role** | Solo full-stack developer: UX, frontend, backend, infrastructure & DevOps |
| **Client** | CoverM Enterprise, LLC · California, USA |
| **Timeline** | Mar 2026 – Oct 2026 |
| **Live** | [covermelienservices.com](https://covermelienservices.com) |

## At a glance

<table><tr>
<td align="center" width="25%"><h3>~40</h3><sub>API endpoints</sub></td>
<td align="center" width="25%"><h3>9</h3><sub>Data models</sub></td>
<td align="center" width="25%"><h3>13</h3><sub>Automated email flows</sub></td>
<td align="center" width="25%"><h3>7 mo</h3><sub>Concept to production</sub></td>
</tr></table>

## The challenge

In California construction, one missed statutory deadline can cost a contractor their lien rights, and the payment that comes with them. The client was taking orders by phone and email, working out deadlines by hand and chasing documents across inboxes. They needed a compliant self-service platform that could quote, take payment and collect documents, and give their team one place to run every case.

## What I built

I designed and built the whole product. It has a Next.js marketing site with California lien-law resources and a free deadline calculator, plus a multi-step intake with server-side pricing and Stripe Checkout. Clients get a secure portal for uploads and requests, and the team gets an admin back office to run each case. It's all deployed on a hardened Linux server with automated CI/CD.

## Key features

### Free deadline calculator

Five quick questions give state-specific lien deadlines in under a minute. The engine applies the earliest rule that matches and skips weekends. It's also the site's strongest lead magnet.

<img src="assets/deadline-calculator.webp" alt="Deadline calculator with five steps: state, project type, role, who hired you and last day on job" width="100%"/>

### Guided intake and Stripe checkout

A three-step intake covers the request, the project and the signature. Pricing is calculated on the server (self-service vs full-service, plus a rush option) and paid through Stripe Checkout with signed, idempotent webhooks. Clients can resume an unpaid request at any time.

<img src="assets/intake-checkout.webp" alt="Intake form with service selection, service levels and secure checkout summary" width="100%"/>

### Secure client portal

Clients track every request, answer document and signature requests, and upload files straight to private, encrypted storage through presigned URLs. Each upload is checked with a checksum and verified by its file signature.

<img src="assets/client-dashboard.webp" alt="Client request center showing request totals, actions needed and membership status" width="100%"/>

### Attorney partner programme

A dedicated area for construction-law firms, with partnership packages and an inquiry pipeline, so attorneys can outsource lien paperwork with confidence.

<img src="assets/attorney-partners.webp" alt="Attorney partnerships page: reliable, construction-focused lien support for law firms" width="100%"/>

## Architecture

```mermaid
flowchart LR
  subgraph L0["Client"]
    direction TB
    L0_0["Browser"]
    L0_1["Cloudflare DNS, proxy & Turnstile"]
  end
  subgraph L1["Edge"]
    direction TB
    L1_0["Nginx reverse proxy"]
    L1_1["Let's Encrypt TLS"]
  end
  subgraph L2["Application"]
    direction TB
    L2_0["Next.js 15 (SSR)"]
    L2_1["Express API /api/v1"]
    L2_2["PDF document worker"]
    L2_3["PM2"]
  end
  subgraph L3["Data & services"]
    direction TB
    L3_0["MongoDB Atlas"]
    L3_1["Private S3-compatible storage"]
    L3_2["Stripe Checkout"]
    L3_3["Resend email"]
    L3_4["AWS SQS"]
  end
  L0 --> L1
  L1 --> L2
  L2 --> L3
```

## Engineering highlights

- JWT in httpOnly cookies with role-based access for clients and admins.
- Per-route rate limits, NoSQL-injection and HTTP parameter pollution protection, and an exact-match CORS allowlist.
- Uploads are SHA-256 checksummed and verified by file signature (magic bytes). Downloads use 60-second signed URLs, issued only after an ownership check.
- Stripe webhooks are signature-verified and deduplicated through a stored event log.
- SMS consent is stored separately from service terms, with a full audit history, and the site carries clear legal disclaimers that it is not a law firm (UPL compliance).
- SEO: canonical URLs, Open Graph, JSON-LD and a generated sitemap. The CI/CD pipeline checks environment values before every deploy.

## Tech stack

| Area | Technologies |
|---|---|
| **Frontend** | ![Next.js 15](https://img.shields.io/badge/Next.js%2015-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![React 18](https://img.shields.io/badge/React%2018-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![SCSS](https://img.shields.io/badge/SCSS-CC6699?style=flat-square&logo=sass&logoColor=white) ![Bootstrap 5](https://img.shields.io/badge/Bootstrap%205-7952B3?style=flat-square&logo=bootstrap&logoColor=white) ![react-simple-maps](https://img.shields.io/badge/react--simple--maps-555?style=flat-square) |
| **Backend** | ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white) ![express-validator](https://img.shields.io/badge/express--validator-555?style=flat-square) ![Helmet](https://img.shields.io/badge/Helmet-555?style=flat-square) ![PDFKit](https://img.shields.io/badge/PDFKit-555?style=flat-square) |
| **Data** | ![MongoDB Atlas](https://img.shields.io/badge/MongoDB%20Atlas-47A248?style=flat-square&logo=mongodb&logoColor=white) ![Mongoose](https://img.shields.io/badge/Mongoose-880000?style=flat-square&logo=mongoose&logoColor=white) ![S3-compatible storage](https://img.shields.io/badge/S3--compatible%20storage-555?style=flat-square) ![AWS SQS](https://img.shields.io/badge/AWS%20SQS-FF4F8B?style=flat-square&logo=amazonsqs&logoColor=white) |
| **Integrations** | ![Stripe Checkout](https://img.shields.io/badge/Stripe%20Checkout-635BFF?style=flat-square&logo=stripe&logoColor=white) ![Resend](https://img.shields.io/badge/Resend-000000?style=flat-square&logo=resend&logoColor=white) ![Cloudflare Turnstile](https://img.shields.io/badge/Cloudflare%20Turnstile-F38020?style=flat-square&logo=cloudflare&logoColor=white) |
| **Infrastructure** | ![Linux VPS](https://img.shields.io/badge/Linux%20VPS-FCC624?style=flat-square&logo=linux&logoColor=000000) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white) ![PM2](https://img.shields.io/badge/PM2-2B037A?style=flat-square&logo=pm2&logoColor=white) ![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) ![CloudFormation](https://img.shields.io/badge/CloudFormation-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white) |

## Screens

<table>
<tr>
<td width="50%" valign="top"><img src="assets/hero.webp" alt="Homepage: California construction lien services" width="100%"/><br/><sub>Homepage: California construction lien services</sub></td>
<td width="50%" valign="top"><img src="assets/how-it-works.webp" alt="How it works: deadline-driven lien workflows" width="100%"/><br/><sub>How it works: deadline-driven lien workflows</sub></td>
</tr>
<tr>
<td width="50%" valign="top"><img src="assets/attorney-services.webp" alt="Support services for construction attorneys" width="100%"/><br/><sub>Support services for construction attorneys</sub></td>
<td width="50%" valign="top"><img src="assets/intake-start.webp" alt="Start a California lien service request" width="100%"/><br/><sub>Start a California lien service request</sub></td>
</tr>
<tr>
<td width="50%" valign="top"><img src="assets/intake-contact.webp" alt="Intake request contact form" width="100%"/><br/><sub>Intake request contact form</sub></td>
<td width="50%" valign="top"><img src="assets/about.webp" alt="About Cover Me Lien Services" width="100%"/><br/><sub>About Cover Me Lien Services</sub></td>
</tr>
</table>

<p align="center"><img src="assets/mobile.webp" alt="Cover Me Lien Services on mobile" width="320"/><br/><sub>Mobile</sub></p>

## About the developer

Designed, built and deployed by **[Shair Ali](https://shairali.com)**, a full-stack developer who owns products end to end: architecture, interface, API, data, payments, servers and CI/CD.

[![Portfolio](https://img.shields.io/badge/Portfolio-shairali.com-111?style=flat-square)](https://shairali.com) [![Fiverr](https://img.shields.io/badge/Fiverr-devshair-1DBF73?style=flat-square&logo=fiverr&logoColor=white)](https://www.fiverr.com/devshair) [![LinkedIn](https://img.shields.io/badge/LinkedIn-shairali2-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shairali2) [![GitHub](https://img.shields.io/badge/GitHub-shairalidev-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/shairalidev)

<sub>Have a similar project? [Get in touch](https://shairali.com/contact).</sub>
