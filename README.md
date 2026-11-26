# Support SLA Triage

A reusable Codex skill that turns support tickets, priority rules, and a service calendar into a reviewable first-response queue.

## Install and run

1. Clone or download this repository. Copy the entire [`support-sla-triage`](support-sla-triage/) folder to `.agents/skills/` in the Codex workspace. The resulting path is `.agents/skills/support-sla-triage/SKILL.md`.
2. Open a fresh Codex session in that workspace. Paste [the DEMO-001 prompt](docs/reworkio-demo.md#demo-001-closure-and-split-service-day), beginning with `$support-sla-triage`.
3. Confirm that Codex returns **High**, a first-response deadline of **2026-12-08 13:15 UTC**, and separate service windows of **45 + 30 + 15 minutes**.

[Reproduce both recorded cases and check the window calculation](docs/reworkio-demo.md). The second input leaves out a receipt time to show how the skill handles incomplete data.

## Use your own policy

Supply the tickets and their receipt timestamps, the ordered priority rules, the SLA budget for each priority, and the service time zone, weekly hours, and exceptions. The skill reports the matched rule and counted windows so a support operator can check the result before using it.

The skill runs on demand inside Codex. The operator supplies the policy and calendar, reviews the result, and handles any missing input. Ticketing system updates and customer notifications happen outside this workflow.
