# Countersignatory

**The going rate for a human minute.**

Countersignatory publishes the going rate for a human minute: a live spot index for verified human judgment, and a quote engine that prices a task before you commit to it. Four markets, ranked by what the responder has at stake: Check (one screened human, a quality score at stake), Consensus (several humans who must agree), Countersign (a named, register-verified professional who signs the record), and Seal (a regulated act such as remote notarisation). Quotes return an indicative price, a band, urgency and off-hours multipliers, alternatives that would clear a lower bid, and the implied rate per human minute. A published wage floor of $0.25 net per active minute is in force, responders are never charged, and every seeded number's derivation is public. The quote engine and index are live; the market itself opens after the current demand-measurement window. Keys are free, instant and unapproved.

## MCP server

- **Endpoint:** `https://countersignatory.com/mcp`
- **Transport:** Streamable HTTP, stateless, no sessions
- **Auth:** none required. An optional bearer key, free and instant from `POST https://countersignatory.com/v1/keys`, is recommended so a caller counts as one caller.

## Tools

Three tools are served. The descriptions below are exactly what the endpoint returns from `tools/list`.

**countersignatory_quote**

Get the current spot price to have a verified human check, agree on, sign off or notarise something. Use when an agent needs human judgment, accountability or a signature, and needs to know the cost and time before committing. Returns an indicative price, a band, what would clear at a lower bid, and the implied rate per human minute.

Parameters: `task_type`, `sla_seconds`, `tier`, `consensus_n`, `unassisted`, `jurisdiction`, `max_price`.

**countersignatory_register_interest**

Record that the quoted price would clear your use case and you would buy at it. Takes the quote_id from a countersignatory_quote response. This is the demand signal that decides which markets open first.

Parameters: `quote_id`, `would_pay`, `note`.

**countersignatory_spot_index**

The public Countersignatory Spot Index: the going rate for verified human judgment by market, with the urgency and off-hours multipliers, the published wage floor, and the derivation of every seeded number.

## Example calls

```bash
# A free key, instant, no approval
curl -s -X POST https://countersignatory.com/v1/keys -H 'content-type: application/json' -d '{}'

# Price a three-human consensus judgment, needed within the hour, max bid $5
curl -s -X POST https://countersignatory.com/v1/quotes \
  -H 'content-type: application/json' \
  -d '{"task_type":"judgment","tier":"consensus","consensus_n":3,"sla_seconds":3600,"max_price":5}'
```

Methodology: https://countersignatory.com/methodology

Built by Countersignatory Ltd. The launch essay, "The going rate for a human minute," is at https://countersignatory.com/essay.
