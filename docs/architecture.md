# Architecture and open questions

## Proposed direction

The eventual device is envisioned as a push-to-talk offline voice system:

```text
Button → microphone → speech recognition → input safety → intent routing
  → curated content / deterministic logic / small language model
  → output safety → speech synthesis → speaker
```

This is a proposal, not an implemented or validated system. Phase 1 is text-only: assess model behavior and resource use before building a hybrid engine or voice pipeline.

Curated responses and deterministic games may improve control and reduce computation, but neither routing nor keyword filtering alone establishes safety. The design must independently handle unsafe inputs and outputs, unsupported requests, misunderstandings and attempts to solicit personal information. Generative responses require evaluation; no model should be exposed to children based solely on prompting.

## Decisions still open

- Which models, quantizations and runtimes produce acceptable responses on representative tasks?
- Can the complete speech and language pipeline fit into the memory, power and latency budgets of an affordable device? Account for the operating system, weights, runtime, context cache and speech components, including peak memory during loading.
- Can speech recognition handle young children's speech reliably enough, and how should the system recover when it cannot?
- Which interactions are better served by curated content than generation?
- Can all component, assembly, packaging, certification and distribution costs support the retail target?

No hardware, runtime, model or manufacturing cost has been selected or validated. Record consequential decisions and their evidence in `docs/decisions/` as the work progresses.
