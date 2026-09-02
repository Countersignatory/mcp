# Countersignatory

**The going rate for a human minute.**

Countersignatory publishes the going rate for a human minute: a live spot index for verified human judgment, and a quote engine that prices a task before you commit to it. Four markets, ranked by what the responder has at stake: Check (one screened human, a quality score at stake), Consensus (several humans who must agree), Countersign (a named, register-verified professional who signs the record), and Seal (a regulated act such as remote notarisation). Quotes return an indicative price, a band, urgency and off-hours multipliers, alternatives that would clear a lower bid, and the implied rate per human minute. A published wage floor of $0.25 net per active minute is in force, responders are never charged, and every seeded number's derivation is public. The quote engine and index are live; the market itself opens after the current demand-measurement window. Keys are free, instant and unapproved.

## MCP server

- **Endpoint:** `https://countersignatory.com/mcp`
- **Transport:** Streamable HTTP, stateless, no sessions
- **Auth:** none required. An optional bearer key, free and instant from `POST https://countersignatory.com/v1/keys`, is recommended so a caller counts as one caller.

## Tools

**countersignatory_quote**

Get the current spot price for verified human input on a task before committing to it: a screened human check, a consensus of several humans, an accountable sign-off by a named register-verified professional, or a regulated notarial act. Use when an agent needs human judgment, verification, approval or a signature and needs the cost and turnaround first. Returns an indicative unit price, a band, the multipliers applied, alternatives that would clear a lower maximum bid, and the implied rate per human minute. Quotes are indicative: the live market has not yet opened and no task is fulfilled.

Parameters: `task_type`, `sla_seconds`, `tier`, `consensus_n`, `unassisted`, `jurisdiction`, `max_price`.

**countersignatory_spot_index**

The public Countersignatory Spot Index: current indicative rates for verified human judgment and accountable sign-off in every open market (Check, Consensus, Countersign, Seal), with urgency and off-hours multipliers, the published wage floor, and the derivation of every seeded number.

## Example calls

    # A free key, instant, no approval
    curl -s -X POST https://countersignatory.com/v1/keys -H 'content-type: application/json' -d '{}'

    # Price a three-human consensus judgment, needed within the hour, max bid $5
    curl -s -X POST https://countersignatory.com/v1/quotes \
      -H 'content-type: application/json' \
      -d '{"task_type":"judgment","tier":"consensus","consensus_n":3,"sla_seconds":3600,"max_price":5}'

Methodology: https://countersignatory.com/v1/methodology

Built by Countersignatory Ltd. The launch essay, "The going rate for a human minute," is at countersignatory.com.
