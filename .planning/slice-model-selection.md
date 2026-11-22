# One implementation agent, several model choices

Planning proposal, not a runtime contract. Keep the agent's role, tools and permissions fixed. Rank eligible **model and reasoning-effort pairs for the slice**, rather than assigning one permanent model to the role. Selection happens before work starts; a fallback after an outage answers a different question.

## What changes the recommendation?

| Slice evidence available before assignment | Example recommendation to test |
|---|---|
| A local precedent exists and a focused acceptance test distinguishes right from wrong. | Start the implementation agent on Terra at its usual effort. Terra has worked well for the operator; this is a baseline, not a universal ranking. |
| The same agent must preserve a rule across several states, such as commit, lost response and retry. | Compare Terra at higher effort with Sol at normal effort. Prefer the least costly pair shown to meet the required reliability. |
| The edit is familiar but a missed defect would be costly. | Keep the implementer; spend on the failure-case test or an independent review. Risk sets the quality floor, not the model name. |
| The intended outcome is disputed. | Return the decision to the operator. Reserve Astra or Fable for explicit major replanning or alignment, outside routine escalation. |

## How to learn the mapping

Public evaluations shortlist candidates; they do not measure success in this project's harness. [METR](https://metr.org/time-horizons/) relates agent success to expert task duration. [RouteLLM](https://arxiv.org/abs/2406.18665) studies when a stronger model adds enough value to justify its cost. [Test-time compute research](https://arxiv.org/abs/2408.03314) motivates testing extra reasoning separately from switching models. None establishes a Concord-specific threshold.

Replay representative historical slices from their pre-change checkout. Give each pair the same brief, tools and acceptance criteria; withhold the finished patch and grading cases. Label slice classes before seeing results. Compare settings on the same slices, then check the resulting rule on different slices. For implementation, report first-pass acceptance, repairs, and total cost per accepted change. For review, use both defective and clean diffs; report consequential misses and false alarms. Do not infer review skill from implementation scores.

Show sample size and uncertainty next to each estimate. Keep billed usage or subscription fee share separate from human repair time unless the operator supplies a conversion rate. If an upgrade costs $0.20 and an avoided repair is worth $10, it needs to prevent more than one repair per 50 slices to save money. That comparison never overrides a required quality floor.

## Fit with the planned ranking

The caller supplies the slice facts and available evidence. Sublector stays offline and returns a JSON ranking, not a dispatch command. Include the role, slice class, eligible model/effort pairs, expected cost, evidence behind the recommendation, and any exclusions. Treat effort as provider-specific. If local evidence is sparse, label a benchmark-only recommendation as uncalibrated; do not present a benchmark percentile as a probability of success.

An acceptance example: submit two briefs for the same implementation agent with fixed permissions and rates. Supply paired results where ordinary Terra meets the quality floor for a patterned edit but only higher-effort Terra or Sol meets it for a retry rule. The rankings should explain the different choices. Remove the local results and both rankings should disclose the missing evidence. Whether slice-conditioned output belongs in the first release remains open; this note does not expand the approved per-agent ranking or authorize live routing.
