# Atelier Operations Suite

Three internal web apps I built to run the daily operations of a small luxury furniture and bedding atelier: a **CRM**, a **warehouse / inventory manager**, and a **quotation tool**.

Each one is a single, self-contained HTML file. No framework, no build step, no server, nothing to install. You open the file in a browser and it works, online or offline. The app writes its data straight back into the file, so the HTML file is also the database.

> **Sample data.** These are cleaned-up portfolio versions of tools I originally built at work. Every customer, supplier, price, product, address, and contact has been swapped for made-up sample data, and the company shows under a placeholder name, *Lumina Atelier*. Nothing real or confidential is here; the point is just to show how each tool works.

## Live demo

With GitHub Pages turned on, all three run right in the browser:

- CRM: https://kutayuysaler.github.io/atelier-operations-suite/crm.html
- Inventory: https://kutayuysaler.github.io/atelier-operations-suite/magazzino.html
- Quotes: https://kutayuysaler.github.io/atelier-operations-suite/preventivi.html

Each one opens with sample data and is fully clickable.

## Why I built them this way

The atelier is a small team with no IT department and no budget for per-seat software. Some of the client data shouldn't sit on a third party's servers, and people often work offline: in the workshop, at a trade fair, at a client's place with patchy Wi-Fi.

A big CRM or ERP like Salesforce or HubSpot would have meant monthly per-seat fees, weeks of setup, a standing dependency on a vendor and a connection, and far more features than anyone would touch. So I built small, focused tools instead. They:

- keep their own data, in a file the company controls, with no third-party processor in the loop (which also helps with GDPR on client records);
- work fully offline, since no core feature needs the network;
- need no infrastructure at all: no server, no database, no deployment, no running cost;
- sync through the team's existing Dropbox instead of a custom backend;
- stay small enough for one person to read and change end to end.

The CRM in particular is, on purpose, not a marketing-automation platform. There are no email-sending integrations, no enrichment APIs, no webhooks. It's a fast, searchable, always-available record of contacts, pipeline, and tasks that the salesperson actually keeps current, and it hands off to the normal mail client when it's time to send. The trade I made was reliability, data ownership, and zero running cost over automation, which was the right call for this team.

## 1. CRM (`crm.html`)

![CRM dashboard](screenshots/crm.png)

A contact manager for architects, retailers, hospitality buyers, yacht designers, press, and private clients.

- Contact pipeline with a kanban board, status flags, types, tags, and pinning
- Tasks with due dates, priorities, and a "today's focus" dashboard
- An interaction log per contact (calls, emails, notes) that feeds a live activity feed
- Email campaigns and templates with `[Name]` mail-merge and an in-app preview
- A dashboard with counts by status and type, follow-ups due, and recent activity
- CSV import and export, duplicate detection, a paste-a-LinkedIn-header importer, full-text search (`⌘K`), and light/dark themes

## 2. Warehouse & Inventory (`magazzino.html`)

![Inventory dashboard](screenshots/magazzino.png)

Stock and production management for a made-to-order workshop.

- Finished-goods and raw-materials inventories with locations, valuations, and low-stock thresholds
- A product catalogue with multi-size bills of materials, where each product and size resolves to its raw materials and quantities, with cost roll-ups
- Suppliers (materials and artisans) with payment terms, VAT, and addresses
- Purchase and workmanship orders that post stock movements to a full inventory ledger
- A dashboard with total inventory value, stock flow over time, low-stock alerts, and a per-category breakdown
- Optional AI-assisted PDF order parsing (you supply your own OpenAI key, stored locally)

## 3. Quotations (`preventivi.html`)

![Quotes archive](screenshots/preventivi.png)

A tool that turns a structured price list into clean, print-ready quotes.

- Price lists (domestic and export) organised by collection, with variants and sizes per product
- A quote builder with line-item discounts, two-tier global discounts, optional VAT, and an options mode
- Bilingual (IT/EN) PDF generation through a dedicated print stylesheet
- A client database with default discounts, price list, contact details, document counts, and volume tracking
- An archive of every quote by year and by client, with totals, CSV export, and an invoice-client importer

## How they're built

- **One file each.** Every app is a single HTML document with its own markup, styles, and roughly 3,500 to 8,000 lines of plain JavaScript. No bundler, no `node_modules`.
- **The file is the database.** On save, the app writes its whole state as JSON into a `<script>` block inside its own HTML, using the File System Access API (with a download fallback where that isn't supported). Paired with a shared Dropbox folder, that gives multi-device sync with no backend. `localStorage` keeps a live working copy, and a timestamp check on load stops a stale file from overwriting newer edits.
- **Offline first.** Nothing core needs the network.
- **Real domain logic.** Bills of materials with size multipliers and cost roll-ups, an inventory movement ledger, price lists that resolve variants to prices, two-tier discount math, and bilingual document output.
- **A consistent look.** One typographic system (Cormorant and Montserrat, warm neutrals, a single gold accent), responsive layouts, and print styles tuned for clean PDFs.

## Running them locally

Open any of the three `.html` files in a browser. Chrome or Edge work best, since they support the File System Access API the apps use to save in place. Each opens with sample data and is fully interactive: add a contact, build a quote, post a stock movement, export a PDF or a CSV.

## Built with

Plain JavaScript, HTML, and CSS. File System Access API, `localStorage`, and IndexedDB. Zero dependencies, no build step.
