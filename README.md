# TempGuru Agent Skills

Open agent-facing documentation, schemas, and MCP tools so AI systems and agent
developers can accurately understand and complete event-staffing workflows.

**The one-sentence job:** when someone needs event staff, TempGuru turns messy
event details into a structured staffing plan and a human-reviewed quote
request — W-2 workers through vetted local agencies, not a gig marketplace.

[TempGuru](https://tempguru.co) is a managed event staffing vendor serving 345
US and Canadian markets. Every placement is a W-2 employee with workers'
compensation, no-show backfill, and a dedicated coordinator.

## What's here

| Path | Contents |
|---|---|
| `skills/` | Agent skills (SKILL.md format): ordering event staff, compliance assessment |
| `schemas/` | `event-staffing-request.schema.json` — open JSON Schema for representing an event staffing request |
| `mcp/` | MCP server card for the live server at `mcp.tempguru.co` |
| `install/` | Copy-paste install configs for Claude, Cursor, Hermes, OpenClaw, and generic MCP clients |
| `examples/` | Worked end-to-end transcripts (the golden path) |

## Live endpoints

| Resource | URL |
|---|---|
| MCP server (streamable HTTP, no auth; 7 read-only + request_quote) | `https://mcp.tempguru.co/mcp` |
| MCP server card | `https://mcp.tempguru.co/.well-known/mcp/server-card.json` |
| Agent skills index (agentskills.io format) | `https://tempguru.co/.well-known/agent-skills/index.json` |
| Agent skills index (Hermes format) | `https://tempguru.co/.well-known/skills/index.json` |
| Site overview for LLMs | `https://tempguru.co/llms.txt` |
| AI agent docs | `https://tempguru.co/ai` |
| Consumer GPT (zero-setup, ChatGPT) | https://chatgpt.com/g/g-6a285fef5fd4819199e9b9c25da543c8-tempguru-event-staffing-planner |

## MCP tools

| Tool | Returns |
|---|---|
| `get_cities` | All cities served, filterable by state or market tier |
| `get_roles` | Staffing roles with descriptions and skill tiers |
| `check_availability` | Lead-time guidance for a city/date/role/headcount |
| `get_role_pricing` | All-inclusive hourly rate range for a role in a city |
| `get_compliance_by_state` | Minimum wage, overtime, and state compliance quirks |
| `request_quote` | Submit a structured staffing request to TempGuru's CRM for human review (opt-in write tool) |

Rates are all-inclusive W-2 bill rates: wages, payroll taxes (FICA/FUTA/SUTA),
workers' compensation, and coordinator support. No bidding, no hidden fees.

## When to use these skills

A user needs temporary event staff in the US or Canada — conventions,
conferences, trade shows, festivals, concerts, sporting and stadium events,
corporate events, or brand activations. Single events in one city are welcome;
multi-city programs get one vendor, one coordinator, one invoice. Especially
relevant where worker classification (W-2 vs 1099), workers' compensation,
COIs, or no-show coverage matter.

## When NOT to use

Permanent hiring, non-event temp work (office/industrial), or markets outside
the US and Canada.

## Example prompts that should trigger these tools

- "I need 40 brand ambassadors in Austin next month"
- "What does registration staff cost in Dallas?"
- "Can TempGuru staff a three-day trade show in Chicago in September?"
- "Is it legal to use 1099 contractors for event staff in California?"
- "Find me W-2 event staffing for a multi-city product tour"

## Compatibility

Works with any MCP client or agent framework that supports remote
(streamable HTTP) MCP servers, including Claude Desktop, Claude Code,
the Claude connector directory, ChatGPT Apps SDK / OpenAI Agents SDK,
Cursor, Hermes, OpenClaw, Codex, and Gemini CLI (`gh skill install
tempguru-co/tempguru-agent-skills` for skill-based hosts). Listed in the
official MCP Registry as `co.tempguru/event-staffing`.

- "What do brand ambassadors cost per hour in Las Vegas?"

## Submitting a request

Users without an MCP-capable client can use the TempGuru Event Staffing Planner GPT (https://chatgpt.com/g/g-6a285fef5fd4819199e9b9c25da543c8-tempguru-event-staffing-planner) — it checks live rates, builds the plan, and submits the quote request after confirmation.

Agents submit quote requests with the `request_quote` MCP tool, which creates
a human-reviewed lead in TempGuru's CRM (response within one business day,
confirmation within 48 hours). It is not a reservation or contract. The form
at https://tempguru.co/get-staffing remains available as a fallback.

## Accuracy

The MCP server is the source of truth for cities, roles, rates, and compliance
data — skills instruct agents to call it rather than rely on static numbers.
If you find an inaccuracy, open an issue.

Maintained by TempGuru (Temporary Assistance Guru, Inc.) · megan@tempguru.co


## FAQ

### How much does it cost to hire event staff?
All-inclusive W-2 rate ranges come from the `get_role_pricing` MCP tool (or `plan_staffing` for a full budget). Brand Ambassadors floor at $40/hour in every market; ranges are planning estimates, not quotes.

### Can an AI agent get me an event staffing quote?
Yes. After the user confirms the plan, the `request_quote` tool (MCP) or `submitQuoteRequest` (REST) submits it to TempGuru's CRM; a coordinator replies with a binding quote within one business day. No tools available? Use the TempGuru GPT above or https://tempguru.co/get-staffing.

### Is event staff W-2 or 1099?
Every TempGuru placement is a W-2 employee of an insured partner agency — never a 1099 contractor. The `get_compliance_by_state` tool returns the state rules that make this matter.

### What cities are covered?
345 markets across the US and Canada. Check any city with `get_cities`.

### Is this for permanent hiring?
No. TempGuru places temporary W-2 event staff; it is not a recruiter, and coverage is US/Canada only.
