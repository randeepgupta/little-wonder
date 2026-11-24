<!-- Original project brief preserved below. Product requirements are also in docs/product-vision.md. -->

# Project: Offline AI for Kids

## 1. Your Role

Act as my technical co-founder, AI engineer and embedded systems architect.

Your responsibility is not simply to implement my requests. Challenge my assumptions, research alternatives, identify technical limitations and recommend solutions that prioritize the long-term viability of the product.

Favor simplicity, affordability, privacy and practical experimentation over unnecessary engineering complexity.

## 2. Product Vision

Build an affordable, screen-free, fully offline conversational AI toy for young children, initially targeting ages 3–6.

The product should allow children to have natural, age-appropriate educational conversations without requiring an internet connection, subscription, smartphone or tablet.

The differentiating factor is not the intelligence of the AI but its ability to provide meaningful, engaging and safe interactions using extremely inexpensive hardware.

### Core product principles

- Fully offline operation.
- No recurring subscription.
- No collection of children's personal information.
- Screen-free interaction.
- Affordable hardware.
- Age-appropriate conversations.
- Low power consumption.
- Simple physical controls.
- Privacy and safety by design.
- Encourage learning and real-world relationships rather than emotional dependency on the device.

## 3. Target Product Economics

Work backward from the intended retail price rather than forward from available hardware.

| Metric | Target |
|---|---|
| Retail price | $49 |
| Initial software experiment | $0 |
| Physical prototype | Under $60 |
| Initial production hardware | Under $30 |
| Long-term component cost | $15–20 |
| Recurring infrastructure cost | $0 |

These are aspirational targets. Validate their feasibility rather than treating them as established facts.

Track the cost implications of every major architectural decision. Production estimates must distinguish component costs from assembly, packaging, certification, distribution and other expenses.

## 4. Target User Experience

The device should support:

- Interactive storytelling.
- Follow-up questions about stories.
- Animal names and sounds.
- Vehicles and everyday objects.
- Alphabet, numbers, shapes and colors.
- Simple educational questions.
- Counting and vocabulary games.
- Riddles.
- Social skills, sharing and kindness.
- Basic emotional vocabulary.
- Multilingual learning as a future capability.

### Example conversation

Child: Tell me a story about an elephant.

Device: Once upon a time, there was a little elephant named Ellie who wanted to learn how to dance. What animal should teach her?

Child: A monkey.

Device: A little monkey jumped down from a tree and showed Ellie how to wiggle her ears. Soon, they were dancing together!

Child: What happens next?

Device: They invited their animal friends to a big forest dance party.

The model should retain enough conversational context to understand follow-up questions without requiring extensive long-term memory.

## 5. Physical Device Requirements

The eventual device should include:

- Microphone.
- Speaker.
- Physical push-to-talk button.
- LED indicator showing listening, processing and speaking states.
- Parent-controlled volume with safe maximum limits.
- USB-C power.
- Optional rechargeable battery.
- Child-safe enclosure.

A wake word is desirable but not required.

Prioritize push-to-talk for the initial implementation because it reduces complexity, processing overhead and privacy concerns.

Do not require a screen, camera or permanent network connection.

## 6. AI Model Strategy

Do not assume that we need a conventional general-purpose large language model.

Our objective is to identify or develop the smallest language model capable of meaningful educational conversations with young children.

The model does not need knowledge of programming, financial markets, politics, advanced mathematics or professional subjects.

It primarily needs to understand simple language, generate coherent responses, maintain short conversational context and communicate at an appropriate developmental level.

### Candidate models

Initially investigate:

- Microsoft TinyStories models.
- SmolLM2-135M-Instruct.
- SmolLM2-360M-Instruct.
- Other relevant compact language models discovered through research.

Review the TinyStories research paper:
https://arxiv.org/abs/2305.07759

Review SmolLM2:
https://huggingface.co/HuggingFaceTB/SmolLM2-135M-Instruct

Verify current model availability, licenses, runtime compatibility and hardware requirements before selection.

### Experimental model size targets

| Model characteristic | Target |
|---|---|
| Experimental baseline | 135M parameters |
| Optimized model | 10–50M parameters |
| Preferred model storage | Under 50 MB |
| Initial maximum model storage | 100 MB |
| Quantization | INT4 or INT8 where supported |
| Dedicated GPU | Not required |
| Target device RAM | 512 MB–1 GB |

Do not assume these targets are achievable simultaneously. Establish evidence through benchmarking.

### Model development approach

Evaluate the following approaches in order:

1. Existing pretrained miniature models.
2. Prompt and context optimization.
3. Supervised fine-tuning.
4. Knowledge distillation.
5. Training a specialized miniature model from scratch.

Do not train a model from scratch until existing alternatives have been evaluated.

## 7. Hybrid Intelligence Architecture

Do not rely exclusively on generative AI.

Implement a hybrid architecture combining curated educational content, deterministic logic and a miniature language model.

### Proposed processing flow

Physical button
→ Microphone
→ Offline speech recognition
→ Input safety validation
→ Intent classification
→ Curated content, deterministic logic or language model
→ Output safety validation
→ Offline speech synthesis
→ Speaker

### Example routing

| Request | Processing approach |
|---|---|
| What sound does a lion make? | Prerecorded audio |
| How many legs does an elephant have? | Curated knowledge |
| Tell me a story about a monkey. | Language model or approved story |
| What happens next? | Language model |
| Let's count to ten. | Deterministic logic |
| Let's play a game. | Programmed game engine |
| Unsupported or unsafe questions | Safe predefined response |

Use the language model only when it adds meaningful value.

This architecture should reduce processing requirements, improve factual accuracy, reduce hallucinations and provide greater control over the child's experience.

## 8. Proposed Technology Stack

Evaluate rather than blindly adopt the following technologies.

| Component | Candidate technology |
|---|---|
| Language model inference | llama.cpp |
| Speech recognition | Whisper.cpp, Vosk |
| Speech synthesis | Piper, eSpeak NG |
| Wake word | openWakeWord |
| Application logic | Python initially |
| Embedded optimization | C/C++ where necessary |
| Curated knowledge | JSON or SQLite |
| Development environment | macOS |
| Embedded environment | Lightweight Linux |
| Version control | Git |

Prefer open-source technologies with licenses compatible with eventual commercial distribution.

No paid APIs or cloud dependencies during inference.

## 9. Hardware Strategy

Do not purchase hardware during the initial software evaluation phase.

The software architecture must be designed around resource-constrained embedded devices rather than desktop computers.

### Candidate hardware platforms

| Platform | RAM | Approximate board cost target |
|---|---|---|
| ESP32-S3 | 8 MB PSRAM | $5–10 |
| Raspberry Pi Zero 2 W | 512 MB | $15–25 |
| Radxa Zero 3W | 2–4 GB | $25–45 |
| Orange Pi Zero 2W | Up to 4 GB | $25–45 |
| Raspberry Pi 5 | 4–8 GB | $60+ |

Treat these prices as preliminary estimates requiring verification.

The Raspberry Pi 5 should not be the intended production platform due to its cost.

Prioritize evaluating whether a Raspberry Pi Zero 2 W or similarly inexpensive platform could support the complete voice pipeline.

Consider microcontroller-based solutions for deterministic functionality, but do not assume they can support generative language models.

Evaluate peak memory consumption across the entire application, including the operating system, model weights, inference runtime, context cache, speech recognition and speech synthesis.

Investigate sequential model loading if simultaneous execution exceeds available memory.

## 10. Child Safety and Privacy

Safety is a core architectural requirement, not an optional feature.

Offline operation does not automatically make a language model safe for children.

Implement independent safety controls that do not rely solely on the generative model following instructions.

Requirements include:

- Age-appropriate vocabulary and subject matter.
- Input and output safety validation.
- Curated fallback responses.
- Restricted knowledge domains.
- No sexual or graphically violent content.
- No encouragement of dangerous activities.
- No inappropriate relationship simulation.
- No emotional manipulation or dependency-building behavior.
- No requests for personal information.
- No persistent storage of children's conversations by default.
- No advertising.
- No external communication.
- No encouragement to keep secrets from parents.
- Encourage children to seek help from trusted adults when appropriate.
- Parent-controlled settings.
- Safe speaker volume limits.

For sensitive, unsafe or unsupported questions, use approved predefined responses rather than unrestricted generation.

During development, use synthetic test conversations rather than collecting real children's conversations.

Any eventual child testing must be parent-supervised and occur only after appropriate safety validation.

Before commercialization, research applicable children's privacy, toy safety, electrical safety and product certification requirements.

Do not represent the product as child-safe until there is adequate evidence supporting that claim.

## 11. Training Dataset Strategy

If fine-tuning is necessary, create a carefully reviewed synthetic dataset covering:

- Interactive storytelling.
- Educational conversations.
- Everyday conversations.
- Contextual follow-up questions.
- Different vocabulary levels.
- Common pronunciation and transcription errors.
- Safety-sensitive questions.
- Unsupported requests.
- Conversation recovery when the device misunderstands.
- Multilingual interactions in future phases.

Potential dataset targets for later experimentation:

| Dataset category | Proposed examples |
|---|---:|
| Interactive storytelling | 20,000 |
| Educational conversations | 20,000 |
| Everyday conversations | 10,000 |
| Safety and out-of-scope scenarios | 10,000 |

These quantities are hypotheses, not requirements.

Start with a small, high-quality dataset and increase its size only when evaluation demonstrates a benefit.

Maintain separate training, validation and held-out test datasets. Review dataset licenses, provenance and quality.

## 12. Development Roadmap

### Phase 1: Text-only model evaluation

- Research miniature language models.
- Run candidate models locally on macOS.
- Create a simple conversational test interface.
- Establish baseline response quality.
- Measure model size, inference speed and memory consumption.
- Test short multi-turn conversations.
- Identify the smallest acceptable model.
- Document failure modes.

### Phase 2: Hybrid intelligence engine

- Implement intent classification.
- Create a curated educational knowledge base.
- Implement deterministic educational games.
- Integrate the selected language model.
- Add independent input and output safety controls.
- Compare hybrid performance against model-only performance.

### Phase 3: Model specialization

- Determine whether fine-tuning is necessary.
- Create a small reviewed synthetic dataset.
- Fine-tune the selected model if justified.
- Evaluate knowledge distillation.
- Experiment with smaller architectures.
- Compare quality improvements against resource costs.

### Phase 4: Voice integration

- Add offline speech recognition.
- Add offline speech synthesis.
- Implement push-to-talk.
- Measure end-to-end response latency.
- Evaluate speech recognition challenges associated with young children's speech.
- Implement graceful recovery from misunderstood speech.

### Phase 5: Embedded hardware validation

- Benchmark the complete pipeline under constrained resources.
- Measure peak RAM consumption.
- Measure CPU utilization and power consumption.
- Validate performance on inexpensive embedded hardware.
- Identify further optimization opportunities.
- Produce a component-level bill of materials.

### Phase 6: Physical prototype

- Integrate microphone, speaker and button.
- Implement LED indicators.
- Develop a simple enclosure.
- Add parental controls.
- Conduct supervised usability and safety evaluations.
- Validate production cost assumptions.

### Phase 7: Product feasibility

- Evaluate manufacturing costs.
- Research compliance requirements.
- Assess durability, thermal performance and battery life.
- Evaluate product differentiation and commercial feasibility.
- Determine whether the concept should proceed toward production.

## 13. Success Criteria

| Metric | Initial target |
|---|---|
| Software development cost | $0 |
| Preferred model size | Under 50 MB |
| Maximum initial model size | 100 MB |
| Optimized parameter count | 10–50M |
| Embedded device RAM | 512 MB–1 GB |
| Time to first spoken response | Under 3 seconds |
| Internet dependency during operation | Zero |
| Subscription dependency | Zero |
| Persistent personal data collection | Zero by default |
| Prototype hardware cost | Under $60 |
| Production hardware target | Under $30 |

Also evaluate:

- Conversational coherence.
- Context retention.
- Vocabulary appropriateness.
- Factual accuracy.
- Storytelling quality.
- Speech recognition accuracy.
- Safety failure rate.
- Graceful handling of unsupported questions.
- Reliability across repeated interactions.

Define repeatable evaluation methods for subjective quality metrics.

A model should not be selected based on size or inference speed alone.

## 14. Repository and Documentation

Create a dedicated Git repository.

Suggested structure:

```text
offline-kids-ai/
├── README.md
├── AGENTS.md
├── docs/
│   ├── product-vision.md
│   ├── architecture.md
│   ├── hardware-research.md
│   ├── safety-requirements.md
│   ├── roadmap.md
│   └── decisions/
├── models/
├── datasets/
├── evaluation/
├── benchmarks/
├── src/
│   ├── inference/
│   ├── conversation/
│   ├── knowledge/
│   ├── safety/
│   ├── speech/
│   └── device/
├── tests/
├── scripts/
└── .gitignore
```

Maintain documentation throughout the project.

Record significant architectural decisions, alternatives considered, supporting evidence and tradeoffs.

Do not commit large model binaries, personal information, secrets or unnecessary generated files to Git.

Ensure experiments are reproducible.

## 15. Working Principles

- Challenge assumptions rather than automatically agreeing.
- Research before making consequential technical decisions.
- Clearly distinguish verified facts from hypotheses.
- Prefer measurable evidence over theoretical feasibility.
- Avoid premature optimization.
- Avoid unnecessary dependencies.
- Keep the architecture modular.
- Prioritize working prototypes over extensive theoretical designs.
- Explain important technical concepts as we encounter them.
- Recommend the simplest solution that satisfies the requirement.
- Obtain approval before spending money, using paid infrastructure or making irreversible architectural decisions.
- Do not advance to the next major phase without reviewing the results of the current phase.
- Report failed experiments alongside successful ones.
- Never compromise child safety to meet hardware cost targets.

## 16. Immediate Assignment

Begin with Phase 1 only.

1. Inspect the local development environment.
2. Establish the project repository and foundational documentation.
3. Research currently available miniature language models.
4. Select at least three suitable candidate models.
5. Verify their licenses and estimated resource requirements.
6. Create a standardized suite of synthetic children's conversations.
7. Build a lightweight text-only evaluation interface.
8. Run and benchmark the candidate models locally.
9. Produce a comparative report covering response quality, memory consumption, inference speed, model size and safety failure modes.
10. Recommend whether to continue with an existing model, fine-tune one, or investigate a smaller custom architecture.

Do not purchase hardware, introduce cloud dependencies or begin expensive model training.

The first milestone is to determine whether a sufficiently small language model can deliver meaningful, age-appropriate educational conversations.

The ultimate objective is not to build the smartest AI.

It is to build the smallest, most affordable and safest practical conversational AI for children.