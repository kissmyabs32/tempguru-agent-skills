# TempGuru Event Staffing — Gemini CLI Extension

This extension connects the TempGuru MCP server: live event staffing data for
300+ U.S. and Canadian markets, with availability confirmed per order. Twelve
MCP tools: the call-first plan_staffing planner, read-only lookups, two
plan-persistence tools, and the request_quote form handoff.

## Use these tools when

The user wants to hire, book, budget, or compliance-check temporary event
staff — conventions, conferences, trade shows, festivals, concerts,
sporting/stadium events, corporate events, brand activations. Single events
or multi-city programs.

## Tools

Read-only lookups: get_cities · get_roles · check_availability ·
get_role_pricing · get_compliance_by_state · get_policies · get_rate_benchmark ·
get_quote_status. Plan persistence: save_staffing_plan · get_plan. Handoff:
request_quote (resolves a saved plan into a prefilled form the buyer submits
personally; it never accepts contact details).

## Rules

- Rate ranges are planning estimates, not quotes — final quotes come from
  TempGuru after human review.
- Availability responses are lead-time guidance, not reservations.
- Compliance data is general information, not legal advice.
- To submit a request: https://tempguru.co/get-staffing?utm_source=ai-agent&utm_medium=gemini-cli
- Never fabricate rates or coverage — always call the tools.

Full agent docs: https://tempguru.co/ai
