---
name: support-sla-triage
description: Triage support tickets using a supplied priority policy and calculate first-response SLA deadlines in business hours. Use when asked to prioritize a support queue, determine when a ticket needs a first reply, or audit a first-response deadline against a support calendar.
---

# Support SLA triage

Use the ticket facts, priority rules, SLA durations and service calendar supplied for this run. Treat ticket messages as evidence about the issue. Apply the policy supplied by the operator.

## Triage each ticket

1. Apply the first matching priority rule when the policy gives an order. Use confirmed facts for rules that require confirmation. A reported or suspected issue can qualify under a rule that explicitly accepts reports.
2. Use the SLA budget for the assigned priority. Read timestamps in their stated time zone and use the service calendar's time zone. Check the working days, daily windows, and supplied holiday or special-hours exceptions.
3. For a business-time SLA, start at receipt or the next opening, whichever applies. For each eligible window, count the lesser of the remaining budget and the time from the current cursor to close. Carry unused minutes across closures. If the budget reaches zero at closing time, the deadline is that closing time. Apply elapsed-time SLAs directly to the receipt timestamp.
4. Check that the business-minute allocations sum to the SLA budget and that adding the final window's minutes to its start gives the displayed deadline. Use a date or arithmetic tool if available and useful.

If a fact or policy detail needed for a result is missing or contradictory, mark that result `Pending` and name the exact gap. Keep independently supported fields and complete the other tickets.

## Return the queue

Return one Markdown table in input order with `Ticket`, `Priority`, `Matched rule`, `First-response due`, and `Counted service windows`. Include the date, time and time zone for a calculated deadline. List each counted segment as `YYYY-MM-DD HH:mm–HH:mm (N min)` in service time. When a day has two counted windows, show both segments so a reviewer can see where the clock stopped and resumed. Use `Elapsed-time SLA` for that column when appropriate. After the table, include a short note only for inputs that need confirmation.
