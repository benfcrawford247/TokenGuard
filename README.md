# TokenGuard

TokenGuard finds and quantifies wasted input-token spend in production AI applications, starting with prompt-caching problems on Anthropic Claude.

> **Status: early development.** There is no working product yet. The source code is private; this repository holds the public project description only.

## What it is being built to do

The first release is a **passive analyser**. It observes requests your application already makes and does all analysis off the request path. It never modifies requests. It is planned to:

- calculate the cost of each request from provider-reported token usage and published list prices;
- explain why prompt caching is not working: unstable prefixes, missing or misplaced cache breakpoints, prefixes too short to cache, and entries expiring between calls;
- estimate the saving from a specific fix, with its assumptions stated;
- flag duplicate requests and retry storms.

## Data handling

By default TokenGuard records token counts, request metadata and keyed hashes (HMAC-SHA-256) of prompt segments. It does not store the text of prompts or responses, and the hashing key stays with the customer.

## How figures are labelled

Every cost figure says what it is:

- **Calculated:** provider-reported usage × published list price. Discounts, credits, committed-use pricing, taxes and currency conversion are excluded.
- **Estimated:** uses an estimated token count or a model, and states its assumptions.
- **Observed change:** the difference between two periods, with no claim about its cause.

No figure is called "actual" or "invoiced" unless it comes from provider billing data. No savings figures are published until they have been measured on real workloads.
