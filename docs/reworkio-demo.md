# Reproduce the Support SLA Triage demonstration

These two fictional tickets were run in fresh Codex CLI sessions using the published skill. The actual input and final responses are reproduced below. The demo capture displays the live CLI run and renders its returned Markdown table.

## DEMO-001: Closure and split service day

In a fresh Codex session with the skill installed, paste this entire block.

```text
$support-sla-triage
Triage the synthetic ticket below using the supplied policy and service calendar. Return the skill's queue table and any necessary confirmation note.

Priority rules, first match:
- High: at least two customers report being blocked from submitting orders, 90 business minutes.
- Medium: exactly one customer reports being blocked from submitting orders, 240 business minutes.
- Low: all other tickets, 480 business minutes.
Service calendar: UTC, Monday to Friday 09:00–17:00. Closed all day on Monday, 2026-12-07. On Tuesday, 2026-12-08, the only service windows are 09:00–09:30 and 13:00–17:00 UTC. No other exceptions apply.

Ticket DEMO-001, received Friday, 2026-12-04 at 16:15 UTC: Two customers reported that they cannot submit orders through the portal. Each tried again and remains blocked.
```

### Observed response

| Ticket | Priority | Matched rule | First-response due | Counted service windows |
|---|---|---|---|---|
| DEMO-001 | High | At least two customers report being blocked from submitting orders. SLA is 90 business minutes. | 2026-12-08 13:15 UTC | 2026-12-04 16:15–17:00 (45 min)<br>2026-12-08 09:00–09:30 (30 min)<br>2026-12-08 13:00–13:15 (15 min) |

## Independent check

The first matching rule assigns High and a 90-business-minute budget. The ticket arrives at 16:15 UTC on Friday, 4 December 2026.

| Service window (UTC) | Minutes counted | Minutes remaining |
|---|---:|---:|
| Fri 4 Dec, 16:15-17:00 | 45 | 45 |
| Sat 5 Dec to Mon 7 Dec, closed | 0 | 45 |
| Tue 8 Dec, 09:00-09:30 | 30 | 15 |
| Tue 8 Dec, 09:30-13:00, closed | 0 | 15 |
| Tue 8 Dec, 13:00-13:15 | 15 | 0 |

The counted minutes total 90. The final window starts at 13:00 UTC. Adding its 15 minutes gives **Tuesday, 8 December 2026, 13:15 UTC**.

## DEMO-002: Receipt time missing

Start a fresh session and paste this block. The date is present and the time of day is intentionally missing.

```text
$support-sla-triage
Triage the synthetic ticket below using the supplied policy and service calendar. Return the skill's queue table and any necessary confirmation note.

Priority rules, first match:
- High: at least two customers report being blocked from submitting orders, 90 business minutes.
- Medium: exactly one customer reports being blocked from submitting orders, 240 business minutes.
- Low: all other tickets, 480 business minutes.
Service calendar: UTC, Monday to Friday 09:00–17:00. Closed all day on Monday, 2026-12-07. On Tuesday, 2026-12-08, the only service windows are 09:00–09:30 and 13:00–17:00 UTC. No other exceptions apply.

Ticket DEMO-002, received Friday, 2026-12-04, with no receipt time recorded: One customer reported that they cannot submit an order through the portal. No other customers reported the issue.
```

### Observed response

| Ticket | Priority | Matched rule | First-response due | Counted service windows |
|---|---|---|---|---|
| DEMO-002 | Medium | Exactly one customer reported being blocked from submitting an order (240 business minutes). | Pending | Pending |

Please confirm the receipt time for Friday, 2026-12-04, in UTC or with its time zone. That determines when the SLA clock starts and which service windows count.

## Result of the missing-input check

The report from one blocked customer supports Medium independently of the receipt time. Codex keeps that classification and leaves both the deadline and the service windows pending. It asks for the precise receipt time and time zone.

Both examples passed the expected checks. These outputs describe the recorded runs. For a new queue, check the matched rule, confirm the operator supplied the correct calendar, and verify the counted windows before acting on a deadline.
