# Sublector

CLI calculations and token economics for multi-agent software development in the `sublection` repository.

> **Status: Design phase.** This repository is in the design and specification phase. No executable code or schema implementations exist yet; the commands, schemas, and workflows below describe planned behavior.

## Problem

Software development workflows increasingly coordinate teams of specialized agents across the full software development lifecycle (SDLC):
- System architects and planners
- Implementers and code generators
- Automated reviewers and verifiers
- Fast lookup, search, and research agents

Operators running these agent fleets often pay for multiple overlapping subscriptions and credit pools (such as Claude Pro/Max, OpenAI Team/Pro, Z.AI coding plans, GitHub Copilot, and pay-as-you-go provider credits). Each plan provides different model access tiers, usage allowances, rate limits, caching discounts, and reasoning token charges.

When an agent orchestrates or configures this pipeline, selecting the right model for each task requires balancing several moving variables:
1. **Entitlements**: Which models are covered under the user's active or evaluated subscriptions?
2. **Benchmark Capability**: How do candidate models score on role-relevant benchmarks (such as the Artificial Analysis Intelligence Index, Coding Index, output speed, and time to first token)?
3. **True Effective Cost**: What does a task actually cost across differing token types (prompt input, cached input read, cache write/creation, output, and separately counted reasoning/thinking tokens)?
4. **Subscription Economics**: At what task volume does a fixed monthly subscription outperform direct API credits, and what is the marginal cost per token?

While agents can look up current model cards, pricing tables, and benchmark scorecards, calculating multi-tier token mathematics, allowance amortizations, and benchmark-to-dollar efficiency inside raw model context is error-prone, noisy, and unstandardized.

## Purpose

Sublector (`sublector`) will be a stateless command-line application built for agents and orchestrators. Given a user's active or considered subscriptions, Sublector will compute model availability, effective token pricing, benchmark scores, and cost-efficiency trade-offs.

## Design Principles

- **Stateless & Deterministic**: Sublector will store no user profiles, credentials, or subscription lists. It will take inputs via command flags or JSON stdin, execute mathematical models, and return structured JSON output.
- **Agent-First Data Retrieval**: Modern coding agents already handle web retrieval, documentation lookup, and live pricing inspection. Sublector will not build scrapers or authenticated third-party API clients. Instead, Sublector will provide:
  - Exact schemas defining what data points an agent should retrieve for subscriptions, model cards, and Artificial Analysis benchmark metrics.
  - Normalized calculation engines to process those retrieved facts reliably.
- **Composable Math**: Calculation functions will be invokable individually or chained together by agent orchestrators to evaluate single prompts, recurring agent roles, or entire subscription portfolios.

## Planned Capabilities

### 1. Retrieval Schemas
Emit machine-readable specifications and field guides so agents know what parameters to extract from provider pricing pages and benchmark boards:
- Subscription structures (base fees, reset windows, included allowances, rate multiplier rules, overage terms)
- Model rate cards (input, cached input reads, cache writes, output, reasoning tokens)
- Benchmark points (Artificial Analysis Intelligence Index, Coding Index, output speed, and time to first token)

### 2. Multi-Tier Token Cost Engine
Compute task and aggregate costs across mixed token compositions:
- Rates for standard input, cached prompt reads, and cache creation
- Rates for completion output and separately counted reasoning tokens
- Normalized effective cost per million tokens ($/Mtok) for realistic prompt-to-cache ratios

### 3. Subscription & Entitlement Evaluation
Calculate effective unit costs and quota dynamics for subscription tiers:
- Marginal token cost inside allowance windows vs. overage rates
- Monthly volume break-even points between subscription tiers and direct API pricing
- Access matrix mapping subscriptions to available models and provider endpoints

### 4. Benchmark-to-Cost Efficiency Index
Pair Artificial Analysis performance metrics with effective token costs to score model efficiency by agent role:
- **Architecture & Planning**: Heavy reasoning scores weighted against large prompt contexts
- **Code Implementation**: Coding benchmark performance weighted against completion and reasoning token costs
- **Review & Verification**: Long-context cache-read efficiency weighted against reasoning accuracy
- **Research & Lookup**: Output speed and time to first token weighted against low-cost input rates

### 5. Portfolio Scenario Analysis
Evaluate combinations of active and considered subscriptions against projected monthly agent workloads, identifying redundant plans, uncovered model tiers, and net cost differences.

## Planned Workflow Example

```bash
# 1. Orchestrator requests Sublector schema
sublector schema --topic subscription,model-rate,benchmarks

# 2. Agent retrieves current subscription terms and Artificial Analysis scores
#    using its native lookup tools.

# 3. Agent pipes retrieved data and workload estimates into Sublector
sublector eval --role implementer < payload.json

# 4. Sublector outputs normalized calculations:
#    - Eligible models across active plans
#    - Effective cost per 1M tokens by token type
#    - Role-weighted benchmark efficiency score
#    - Recommendation metrics for model assignment
```

## License

[MIT](LICENSE)
