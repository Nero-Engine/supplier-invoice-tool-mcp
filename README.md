# Supplier Invoice Tool

Turns a UK trade business's supplier invoices (CEF, Edmundson, Screwfix, Toolstation and others) into one draft Xero bill per supplier per month, one line per job, with the originals kept and price rises flagged.

**Endpoint:** `https://supplier-invoice-tool.nerolabs.workers.dev/mcp` (MCP, Streamable HTTP)
**Sign-in:** A private key per business. The first call (create_trade_account) returns it once; every later call sends it as the header "Authorization: Bearer <key>". Xero is connected separately by the business signing in to Xero.
**Status:** Test mode. Free while it is tested. Only a Xero Demo Company can be connected until the Xero link is approved.
**How to connect:** https://supplier-invoice-tool.nerolabs.workers.dev/docs
**Privacy:** https://supplier-invoice-tool.nerolabs.workers.dev/privacy
**Support:** founder@neroengine.com

## Tools

| Tool | What it does |
|---|---|
| `create_trade_account` | Create the business invoice book. Start here, once per business. |
| `get_account` | Show the business account and settings. The trade's account, settings and Nero identity. |
| `update_settings` | Change job reference and Xero settings. Change how job references are read and how bills are entered in Xero. |
| `add_supplier_invoices` | Add supplier invoices (emails, PDFs, photos). Add supplier invoices to the book: raw emails with PDF attachments, PDFs (text or scanned), photos, or pasted text, up to 25 per call. |
| `month_summary` | Month summary: draft bills per supplier and job. The month at a glance: one draft bill per supplier with a line per job (net, VAT and which invoices), invoices held back to check, lines with no job reference, and price changes with the extra cost they caused. |
| `list_invoices` | List the month's invoices. Every invoice in the book for a month, with its lines, status and any problems. |
| `price_alerts` | Supplier price changes this month. Price changes on the same product code from the same supplier this month, in date order, and the extra they cost. |
| `get_original` | Link to an original invoice. A private link to the original email, PDF or scan of one invoice, to show the trade. |
| `assign_job_reference` | Put an invoice on a job. Put an invoice (or some of its lines) on a job, when the supplier left the reference off or it was wrong. |
| `review_invoice` | Accept or remove an invoice held for checking. For an invoice held back as needs_check: accept it as read (it then goes on the bill), or remove it (for example to add a corrected copy). |
| `connect_xero` | Get the Xero sign-in link. A link for the trade to open and sign in to Xero. |
| `xero_status` | Check the Xero connection. Whether Xero is connected, and to which organisation. |
| `push_bills_to_xero` | Put the month's bills into Xero as drafts. Put the month's bills into Xero as DRAFT bills, one per supplier, one line per job, with the original invoices attached. |
| `disconnect_xero` | Forget the Xero connection. Forget the Xero connection. |

Every tool carries a plain title and the read-only, destructive and open-world hints, so your AI app can ask before anything that changes data.

## Connect

- **Claude Code:** `claude mcp add --transport http supplier-invoice-tool https://supplier-invoice-tool.nerolabs.workers.dev/mcp --header "Authorization: Bearer <key>"`
- **Cursor, VS Code and others:**

```json
{ "mcpServers": { "supplier-invoice-tool": { "type": "http", "url": "https://supplier-invoice-tool.nerolabs.workers.dev/mcp", "headers": { "Authorization": "Bearer <key>" } } } }
```

Claude.ai and ChatGPT custom connectors cannot send a fixed key header yet, so this tool does not work there yet.

## Try asking

- "Set up my invoice book: Spark and Sons Electrical Ltd, VAT registered, job numbers start JOB."
- "Here are this month's CEF and Screwfix invoice emails. Add them and tell me which ones need checking."
- "Show me November's bills per supplier and any price rises, then do a dry run of the Xero push."

## Good to know

- Bills only ever go into Xero as drafts. The business approves them in Xero. Nothing is paid, approved or emailed by this tool.
- Text inside an invoice is treated as data, never as instructions.
- Free. No card and no paid plan while in test mode.

## Privacy

What is kept, what is never kept, and how to get data deleted: https://supplier-invoice-tool.nerolabs.workers.dev/privacy. Usage counts log the tool name, time, AI app name, country and a one-way scrambled caller code; never your questions, the answers or IP addresses.

This repository holds the listing only (README and server.json). The server runs at the endpoint above.

Built by Nero Labs (Nero Engine Group Ltd, UK).
