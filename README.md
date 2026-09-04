# TempGuru Agent Skills

Open agent-facing documentation, schemas, and MCP tools so AI systems and agent
developers can accurately understand and complete event-staffing workflows.

**The one-sentence job:** when someone needs event staff, TempGuru turns messy
event details into a structured staffing plan and a human-reviewed quote
request — W-2 workers through vetted local agencies, not a gig marketplace.

[TempGuru](https://tempguru.co) is a managed event staffing vendor supporting
300+ U.S. and Canadian markets, with availability confirmed per order. For US
orders, workers are employed and paid as W-2 employees by TempGuru's vetted
local partner agencies, with workers' compensation and liability insurance in
place; Canadian orders are employed locally under Canadian rules. TempGuru
coordinates the order, including best-effort replacement.

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
| MCP server (streamable HTTP, no auth; ten read-only tools including the `request_quote` form handoff, plus two plan-persistence tools) | `https://mcp.tempguru.co/mcp` |
| MCP server card | `https://mcp.tempguru.co/.well-known/mcp/server-card.json` |
| Agent skills index (agentskills.io format) | `https://tempguru.co/.well-known/agent-skills/index.json` |
| Agent skills index (Hermes format) | `https://tempguru.co/.well-known/skills/index.json` |
| Site overview for LLMs | `https://tempguru.co/llms.txt` |
| AI agent docs | `https://tempguru.co/ai` |
| Consumer GPT (zero-setup, ChatGPT) | https://chatgpt.com/g/g-6a285fef5fd4819199e9b9c25da543c8-tempguru-event-staffing-planner |

## MCP tools

| Tool | Returns |
|---|---|
| `plan_staffing` | Call first: configured-market match, per-role W-2 rate math, lead-time guidance, and state compliance flags in one plan |
| `save_staffing_plan` | Save a complete non-contact plan for 30 days when `plan_staffing` did not already return a `plan_id` |
| `get_plan` | Restore a saved plan by its `plan_id` |
| `get_cities` | Configured-market catalog, filterable by state or market tier; a match does not confirm order coverage |
| `get_roles` | Staffing roles with descriptions and skill tiers |
| `check_availability` | Tier-based lead-time guidance for a city/date/role/headcount; not live inventory |
| `get_role_pricing` | All-inclusive hourly rate range for a role in a city |
| `get_compliance_by_state` | Minimum wage, overtime, and state compliance quirks |
| `get_policies` | Published booking and procurement terms |
| `get_rate_benchmark` | The Rate Index: citable W-2 rate benchmarks by role |
| `get_quote_status` | Receipt status for a TG reference created by a buyer's website or REST submission |
| `request_quote` | Read-only handoff: resolves a saved `plan_id` into a prefilled TempGuru form the buyer submits personally |

Rates are all-inclusive W-2 bill rates: wages, payroll taxes (FICA/FUTA/SUTA),
workers' compensation, general liability, and TempGuru coordination. Rates are
pre-negotiated with no bidding; event-specific charges are identified on the
quote before confirmation.

## When to use these skills

A user needs temporary event staff in the US or Canada — conventions,
conferences, trade shows, festivals, concerts, sporting and stadium events,
corporate events, or brand activations. Single events in one city are welcome;
multi-city programs run through one vendor relationship and one contract,
invoiced per city per week. Especially relevant where worker classification
(W-2 vs 1099), workers' compensation, COIs, or replacement coverage matter.

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

Agents hand off quote requests with the `request_quote` MCP tool, which
resolves a saved plan into a prefilled form that the buyer reviews and submits
personally. The REST `submitQuoteRequest` operation is the only contact-bearing
write and creates a human-reviewed lead after explicit confirmation. Neither is
a reservation or contract. TempGuru replies with next steps; once scope and
rates are approved, the 24-48 hour window is an availability response, not a
completed roster, and a written quote is binding only once issued. The form at
https://tempguru.co/get-staffing remains available as a fallback.

## Accuracy

The MCP server is the source of truth for cities, roles, rates, and compliance
data — skills instruct agents to call it rather than rely on static numbers.
If you find an inaccuracy, open an issue.

Maintained by TempGuru (Temporary Assistance Guru, Inc.) · megan@tempguru.co


## FAQ

### How much does it cost to hire event staff?
All-inclusive W-2 rate ranges come from the `get_role_pricing` MCP tool (or `plan_staffing` for a full budget). Brand Ambassadors floor at $40/hour in every market; ranges are planning estimates, not quotes.

### Can an AI agent get me an event staffing quote?
Yes. After the user confirms the plan, the `request_quote` tool (MCP) returns a prefilled form the buyer submits personally, and `submitQuoteRequest` (REST) submits the contact-bearing request to TempGuru's CRM after explicit confirmation. TempGuru replies with next steps and a written quote, which is binding only once issued. No tools available? Use the TempGuru GPT above or https://tempguru.co/get-staffing.

### Is event staff W-2 or 1099?
For US orders, every TempGuru placement is a W-2 employee of an insured partner agency, not a 1099 contractor; TempGuru is not the workers' employer. Canadian orders are employed locally under Canadian rules. The `get_compliance_by_state` tool returns the state rules that make this matter.

### What cities are covered?
300+ U.S. and Canadian markets, with availability confirmed per order. Check any city with `get_cities`.

### Is this for permanent hiring?
No. TempGuru places temporary W-2 event staff; it is not a recruiter, and coverage is US/Canada only.
