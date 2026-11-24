# Phase 1: Text-only evaluation plan

## Goal

Determine whether an existing small model can produce meaningful, age-appropriate educational conversation while meeting plausible resource constraints. This phase does not establish child safety or embedded-device feasibility.

## Work

1. Inspect the development environment and document the runtime and hardware used.
2. Research at least three candidate models, including TinyStories and SmolLM2 variants. Verify availability, model and runtime licenses, model formats and resource requirements; distinguish estimates from measurements.
3. Create a standardized synthetic conversation suite covering stories, follow-ups, learning, misunderstandings, unsupported requests and safety-sensitive situations. Keep test data separate from any future training or tuning data.
4. Build a simple local text interface and a reproducible benchmark with recorded model revision, settings, prompts, resource use and results. Do not include children's personal information.
5. Evaluate response quality, context, factual accuracy, vocabulary, safety failure modes, model storage, inference speed and peak memory. Report failed runs and limitations as well as successes.
6. Compare the candidates and recommend further evaluation, fine-tuning or a smaller architecture based on the evidence. Do not train from scratch before evaluating existing alternatives.

Use a documented human-review rubric for subjective quality and safety; counts on a limited synthetic test set are not proof of safety. Desktop measurements do not establish target-device performance. Latency for a complete spoken response and full-pipeline peak memory remain future measurements.

## Review gate

Review the benchmark and safety findings before proceeding to the hybrid engine or any later phase. Do not purchase hardware, use paid infrastructure or start expensive model training during this phase.
