# Sample Tool Outputs

Illustrative response shapes for the five MCP/REST tools. **These are
examples of structure, not current data — always call the live tools for
real numbers** (`https://mcp.tempguru.co/mcp` or the REST mirror).

## get_role_pricing (verified example, June 2026)

Request: `role=brand-ambassadors, city=boston`

```json
{
  "input": { "role": "brand-ambassadors", "city": "boston" },
  "city": "Boston",
  "tier": "hub",
  "role": "Brand Ambassadors",
  "rate_range": { "min": 56, "max": 65, "currency": "USD", "unit": "hour" },
  "rate_includes": "W-2 wages, payroll taxes (FICA/FUTA/SUTA), workers' compensation, TempGuru coordination"
}
```

Agent framing: "Brand ambassadors in Boston run $56–$65/hr all-inclusive as a
planning estimate — the final quote comes from TempGuru's coordinator."

## check_availability

Returns lead-time guidance keyed to market tier (hub ≈ 48h confirmation,
mid ≈ 72h, small ≈ 1 week), plus notes. Not a reservation.

## get_cities

Returns city list with `tier` (hub/mid/small), filterable by `state` or
`tier`. Use to confirm coverage before planning.

## get_roles

Returns role slugs, display names, descriptions, and skill tiers. Use the
slugs verbatim in `get_role_pricing` calls.

## get_compliance_by_state

Returns minimum wage, overtime threshold, and state-specific quirks
(e.g., California ABC test notes). General information, not legal advice.

## Error shape (REST)

```json
{
  "error": {
    "code": "not_found",
    "message": "Unknown role \"astronaut\". Available roles: ...",
    "field": "role",
    "suggestion": { "kind": "role", "slug": "setup-breakdown" }
  }
}
```

Errors include did-you-mean suggestions — use them to self-correct rather
than asking the user.
