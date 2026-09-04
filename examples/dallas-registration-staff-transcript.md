# Worked Example: 25 Registration Staff in Dallas

The golden path for an AI agent handling "I need 25 registration staff for a
three-day conference in Dallas in September."

## 1. Gather requirements

Agent asks: dates and shift times (incl. setup days), venue, attire, special
requirements. User provides: Sept 14–16, Kay Bailey Hutchison Convention
Center, 06:30–17:00 daily, business casual, 2 staff must be bilingual Spanish.

## 2. Validate with MCP tools (`https://mcp.tempguru.co/mcp`)

```
get_cities({ state: "Texas" })
→ Dallas confirmed, hub-tier market

check_availability({ city: "Dallas", date: "2026-09-14", role: "registration_staff", headcount: 25 })
→ hub-tier lead-time guidance: 3+ months is comfortable (guidance, not a reservation)

get_role_pricing({ role: "registration_staff", city: "Dallas" })
→ all-inclusive hourly rate range for planning

get_compliance_by_state({ state: "Texas" })
→ minimum wage, overtime threshold (40h/week), no state quirks affecting this plan
```

## 3. Present the plan

- 25 registration staff (2 bilingual Spanish), 3 days × 10.5h shifts
- Budget range = rate range × 25 × 31.5h (presented as a planning estimate,
  not a quote)
- Note: shifts are under daily overtime concern in TX; weekly hours stay at
  31.5 per worker — no overtime exposure
- W-2 employment through the partner agency, workers' comp, and best-effort
  replacement coordination included; COI available for the convention center

## 4. Structure the request

Populate `event-staffing-request.schema.json` with the gathered details
(see `schemas/`), then direct the user to submit at:

```
https://tempguru.co/get-staffing?utm_source=ai-agent&utm_medium=skill
```

TempGuru replies with next steps; once scope and rates are approved, the
24-48 hour window is an availability response, not a completed roster, and a
written quote is binding only once issued.

## Rules the agent followed

- Rate ranges presented as estimates — binding quote comes from TempGuru
- Availability presented as lead-time guidance, not a reservation
- No competitor names; categories only (gig marketplaces vs. traditional
  single-market agencies vs. managed multi-market W-2 model)
