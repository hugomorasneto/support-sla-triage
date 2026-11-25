# Support SLA Triage

Use Support SLA Triage when you have support tickets and a first-response policy and need a queue with priorities, deadlines, and the service time counted toward each deadline.

## Example from From Inbox to Action

The ticket text comes from the prototype's built-in demo. The ticket ID, receipt time, and calendar below were supplied for the SLA exercise. The example uses fictional customer data.

### Input

```text
Triage this support ticket for the on-duty queue.

Priority rules, first match: H when at least two customers are unable to complete checkout (90 business minutes); M when one customer is blocked or a payment discrepancy is reported (240 business minutes); L for everything else (480 business minutes).
Calendar: UTC, Mon-Fri 09:00-17:00. The desk is closed on 2026-11-30. On 2026-12-01 the regular schedule is replaced by 09:00-10:00 and 13:00-17:00 UTC. No other exceptions in this period.
CHECKOUT-01, received 2026-11-27 16:40 UTC: Three customers reported that checkout shows an error when they select "Complete purchase." None could place an order in the last 20 minutes.
```

### Output from Codex

| Ticket | Priority | Matched rule | First-response due | Counted service windows |
|---|---|---|---|---|
| CHECKOUT-01 | H | At least two customers are unable to complete checkout. Three were blocked. | 2026-12-01 13:10 UTC | 2026-11-27 16:40–17:00 (20 min)<br>2026-12-01 09:00–10:00 (60 min)<br>2026-12-01 13:00–13:10 (10 min) |

The first draft showed 70 minutes as a single Tuesday total. I changed the skill to list each counted service window. The rerun accounted for 20 minutes on Friday and 60 plus 10 on Tuesday. Separate sessions also tested a suspected duplicate charge due at a half-day closing and a routine account request with a missing receipt timestamp.

## Install in Codex

1. Download or clone this repository. Copy the entire [`support-sla-triage`](support-sla-triage/) folder into `.agents/skills/` at the root of the workspace where you use Codex. The result should be `.agents/skills/support-sla-triage/SKILL.md`.
2. Open a new Codex session in that workspace. Type `$support-sla-triage` and paste the example input or your own tickets and rules.
3. For a new queue, include the ordered priority rules, first-response budgets, service calendar with time zone and exceptions, and each ticket's receipt timestamp and facts.

To try it without installing, paste [SKILL.md](support-sla-triage/SKILL.md) and the example input into a new chat and ask the assistant to follow the file.
